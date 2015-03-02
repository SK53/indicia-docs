Custom Cache Tables
-------------------

The Custom Cache Tables module allows for optimisation of reports by preparation of interim tables which cache data 
that would otherwise need to be calculated on the fly during reporting. The module does nothing on its own but requires
additional files to define the queries and associated scheduling information. Tables are created in a database schema 
called ``custom_cache_tables``.

In order to create a custom cache table, first decide on the name of your table. In order to ensure that your table 
name is unique, please prefix your table name to uniquely identify the website it belongs to. Table names should be 
lowercase with underscores. Now, create a file called *mytablename*.php in the warehouse 
``modules/custom_cache_tables/definitions`` folder replacing *mytablename* with your real table name. In this file, 
you need to write 2 PHP functions (replacing mytablename as before):

.. code-block:: php

  /**
   * Return some metadata about the custom cache table which helps the warehouse decide when to rebuild it.
   */
  function get_mytablename_metadata() {
    return array(
      // How long should the warehouse wait between checking if an update is required? Examples could be
      // '30 minutes', '6 hours', '2 days' etc.
      'frequency' => '1 hour',
      // Provide an optional count query that picks up the number of changes in the database that would impact 
      // on the contents of the cache table since a date stamp, e.g. the number of changes to samples in your survey.
      // The token #date# will be replaced at run time with the date stamp of the previous check. If this query 
      // is omitted then the cache table is rebuilt every time the timespan above passes. In this example
      // we test for new samples in our survey (ID 200)
      'detect_changes_query' => 'select count(*) from samples where survey_id=200 and updated_on>'#date#'
    );
  }
  
  /** 
   * Define the query used to build the custom cache table. In this example we count the number of 
   * samples per location in a location layer. Note that the query is a select ... into query which 
   * creates the required table.
   */
  function get_mytablename_query() {
    return <<<'QRY'
      select l.id, l.name, count(s.id)
      into custom_cache_tables.mytablename
      from locations l 
      left join samples s on s.deleted=false and s.survey_id=200
        and st_intersects(s.geom, l.boundary_geom)
      where l.location_type_id=100 and l.deleted=false
  QRY;
  }

The warehouse scheduled tasks will now rebuild the cache table at the desired frequency.

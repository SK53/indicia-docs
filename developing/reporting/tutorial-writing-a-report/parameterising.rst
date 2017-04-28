Parameterising the report
-------------------------

As well as the simple column filtering, it is possible to declare named
parameters that must be input into a form before the report is run. To do this
requires a ``<params>`` element in the XML document at the same level as the
``<columns>`` and ``<query>`` elements. This new element contains a single
``<param>`` element for each parameter you want to declare. Each parameter has
attributes for the **name**, **display** (the display label), an optional
**description** and a **datatype**. There are other attributes but these are the
ones required for basic parameterisation. The parameter's name is wrapped with a
# either side to make a replacement token which is then applied to the report
query. As an example add the following parameters block to your report file in
the appropriate place, plus update your where statement in the SQL to include
the following filter using the following parameter and try it out:

.. code-block:: xml

  <params>
    <param name="quality" display="Data quality" datatype="lookup"
        description="Quality level required of data to be included in the map."
        lookup_values="V:Data must be verified,C:Data must be verified or certain,
            L:Data must be at least likely,!D:Include anything not dubious or rejected,
            !R:Include anything not rejected" />
  </params>

The parameter uses a lookup datatype to create a drop-down selection in the parameters
form for the quality required of the records to include. Each entry is separated
by a comma, with the actual value used preceding the colon and the label
displayed to the user after the colon. We also need some SQL which uses the new
quality parameter, so insert the following code into the very end of the
``<query>`` element so it forms the last line of the ``where`` clause:

.. code-block:: sql

  and quality_check('#quality#', o.record_status, o.certainty)=true

Note that we are using the ``quality_check`` function, which Indicia adds to the
functions available in PostgreSQL in order to provide an easy way to filter
records by the verification status and record certainty. You should find now
that when you load the report in your Drupal site you are presented with a
parameters input form as follows:

.. image:: ../../../images/screenshots/tutorials/report-data-quality-parameter.png
  :width: 800px
  :alt: The Data Quality input parameter for our report.

Try selecting different options for the Data quality parameter to see what
happens when you run the report. If you are stuck, here is the full text of the
report at this stage:

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
  <report title="Tutorial"
      description="Display some records for the report writing tutorial">
  <query website_filter_field="o.website_id">
    select #columns#
    from cache_occurrences_functional o
    join cache_samples_nonfunctional snf on snf.id=o.sample_Id
    join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
    #agreements_join#
    where #sharing_filter#
    and o.created_on&gt;now()-'1 month'::interval
    and quality_check('#quality#', o.record_status, o.certainty)=true
  </query>
  <params>
    <param name="quality" display="Data quality" datatype="lookup"
           description="Quality level required of data to be included in the map."
           lookup_values="V:Data must be verified,C:Data must be verified or certain,
          L:Data must be at least likely,!D:Include anything not dubious or rejected,
          !R:Include anything not rejected" />
  </params>
  <columns>
    <column name="id" sql="o.id" visible="false" datatype="integer"/>
    <column name="public_entered_sref" sql="snf.public_entered_sref"
            display="Grid Ref" datatype="text"/>
    <column name="preferred_taxon" sql="cttl.preferred_taxon"
            display="Species" datatype="text"/>
    <column name="default_common_name" sql="cttl.default_common_name"
            display="Common Name" datatype="text"/>
    <column name="date_start" sql="o.date_start" visible="false"/>
    <column name="date_end" sql="o.date_end" visible="false"/>
    <column name="date_type" sql="o.date_type" visible="false"/>
    <column name="date" display="Date" datatype="date"/>
  </columns>
  </report>

You can also set an attribute called ``default`` on the ``param`` element to one of the
possible values. If you do this then the report will load immediately without showing the
parameter input form, but the parameter remains available for overriding through the
configuration options on the page. E.g. you could set default="!D" in this instance to
allow the report to load immediately.

.. tip::

  It's also possible to use the population_call attribute to create a list of
  options for the parameter drop-down via a query against the database.

Standard parameters
^^^^^^^^^^^^^^^^^^^

Using the technique above, each report in the library can have a different unique set of
parameters. There are advantages, however, to enabling a standardised set of parameters
allowing different reports to be treated in the same way by the calling code, for example
it make development much easier if you can be sure that all reports will respond to a date
range and polygon filter. To use the standard parameters features your report must fulfill
certain criteria:

  * The report must include the cache_occurrences_functional table in the query with the
    table alias set to "o". This way all the parameters can use the same SQL to work.
  * The report must include the following replacement tags after the section which refers
    to the cache_occurrences_functional table (i.e. at the end of the list of JOIN
    statements):

      * #agreements_join# - joins to tables that relate to enforcing permissions
      * #joins# - other joins will be dynamically inserted here depending on the filter
        parameters used.

    * The WHERE clause of the report must include the following tags and not have an ORDER
      BY or GROUP BY after it (which will be dynamically generated):

      #sharing_filter#
      #idlist#

    * Add an attribute called ``standard_params`` to the ``<query>`` element and set the
      value to "occurrences" (there is a similar, more limited set of parameter that works
      with queries that only deal at the sample level which can be triggered by setting the
      value to "samples" and including cache_samples_functional in the query).

Here's our report modified for use with the standard parameters:

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
  <report title="Tutorial"
      description="Display some records for the report writing tutorial">
    <query website_filter_field="o.website_id" standard_params="occurrences">
      select #columns#
      from cache_occurrences_functional o
      join cache_samples_nonfunctional snf on snf.id=o.sample_Id
      join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
      #agreements_join#
      #joins#
      where #sharing_filter#
      #idlist#
    </query>
    <columns>
      <column name="id" sql="o.id" visible="false" datatype="integer"/>
      <column name="public_entered_sref" sql="snf.public_entered_sref"
              display="Grid Ref" datatype="text"/>
      <column name="preferred_taxon" sql="cttl.preferred_taxon"
              display="Species" datatype="text"/>
      <column name="default_common_name" sql="cttl.default_common_name"
              display="Common Name" datatype="text"/>
      <column name="date_start" sql="o.date_start" visible="false"/>
      <column name="date_end" sql="o.date_end" visible="false"/>
      <column name="date_type" sql="o.date_type" visible="false"/>
      <column name="date" display="Date" datatype="date"/>
    </columns>
  </report>

To make use of the standard parameters approach in Drupal:

  #. Add a new content page of type **Indicia pages**.
  #. Set the title & menu item as before.
  #. Choose the page category **Reports** and the page type **Reporting page
     (customisable)** then click **Load Settings Form**.
  #. Under the **User Interface** section, set the **Form Structure** to::

       [standard params]
       [reportgrid]
       @dataSource=<path to my report, excluding .xml suffix>

  #. Under the **Report Settings** section, clear the settings in the **Preset parameter
     values** and **Default parameter values** sections.
  #. Save the page and you should find that there is a filter bar above your report table
     with a **Create a filter** button and lots of functionality that can only work because
     we can depend on the full set of standard parameters being available.

For more information on standard parameter functionality, see
:doc:`../standard-parameters`.

***********************
Data Model Introduction
***********************

Indicia's database is a traditional relational database based on PostgreSQL with spatial
extensions supported by PostGIS. The database tables and columns are documented in the
schema comments. Here's an introduction to some key ares of the data model to get you
started with querying the database.

websites > surveys > samples > occurrences
==========================================

The main spine of the data model captures species observations and is covered by the
websites,  surveys, samples and occurrences tables.

websites
--------

All occurrence data in the database are "owned" by the client website which they were
entered on. Each client website has an entry in the websites table which allows all the
records to be  tagged against the website ID which contributed them. By default each
website can only view or edit the occurrence data belonging to them, though it is also
possible to set up agreements between registered websites that allow the records to be
shared. For example,  this approach is used to allow multiple websites to share their
records to the iRecord verification portal in the UK.

surveys
-------

Within each website registered on the warehouse, data are divided up into survey datasets,
each described by a single row in the surveys table. Each survey dataset can have a
different set of attributes collected for the records it contains so it makes sense to
divide the records into multiple survey datasets based on their purpose and data structure
rather than to keep them all together in one. For example, a survey dataset for insect
data might collect an attribute for the count of each record, whereas one for plant
data might collect a DAFOR abundance value. The configuration of custom attributes
available is defined at the level of the survey dataset therefore it is often the case that
a survey dataset is created for each recording form you build.

samples
-------

A sample defines a set of data which were collected by the same recorder(s) on the same
date at the same place using the same method. Therefore you would expect to have a sample
record created for each grid reference you recorded at during a day of recording. Each
sample can contain any number of occurrences (records) and each sample belongs to a
survey dataset which defines the additional custom attributes available to record against
it.

Note that samples can be hierarchical by pointing the parent_id foreign key field at
another sample record. This allows more complex surveying methodologies to be captured,
for example a transect sample can capture metadata about the overall transect, then
sub-samples can capture the records at exact points along the transect.

.. tip::

  Since a sample date can span several days, or may not be precisely known (especially
  relevant for historic data), sample dates are stored in a 3 field "vague date format"
  borrowed from Recorder. The first 2 fields are a date_start and date_end field which
  define the complete range of dates covered by the vague date. They will be the same if
  a single exact date is provided and one or the other can be null (e.g. when specifying
  a date before 2009 the start date will be null). The 3rd date_type field is a code which
  describes what type of date is being given, e.g. an exact day, month, year or date range.
  You can use the `vague_date_to_string(date_start, date_end, date_type)` function to
  convert the date stored in the database into formatted text for display.

occurrences
-----------

Each occurrence of a species recorded in the database is stored as a single record in the
occurrences table. Occurrences always belong to samples, have a foreign key to the taxon
and may have additional custom attributes attached, e.g. for the abundance count.

The following example illustrates this section of the database schema by selecting some
simple details from the most recently added record in the database. Note it doesn't include
any taxonomic information - we'll cover that in a moment.

.. code-block:: sql

  select o.id,
    w.title as website_title,
    su.title as survey_title,
    s.entered_sref,
    vague_date_to_string(s.date_start, s.date_end, s.date_type) as "date"
  from websites w
  join surveys su on su.website_id=w.id and su.deleted=false
  join samples s on s.survey_id=su.id and s.deleted=false
  join occurrences o on o.sample_id=s.id and o.deleted=false
  where w.deleted=false
  order by o.id desc
  limit 1

taxon_lists > taxa_taxon_lists > taxa
=====================================

The second key part of the database is the taxonomy module which captures information
about the species and other taxa which you can record against.

taxon_lists
-----------

The database stores multiple lists of taxa. A list can be anything from a simple flat list
of a few species being recorded by a citizen science project to a full hierarchical
taxonomy for a country's species list.

taxa_taxon_lists
----------------

The taxa_taxon_lists table serves to join taxa to the lists they belong to.

taxa
----

The taxa table contains one row per taxon name. A single species concept, therefore, may
have several rows in the taxa table, with one for the currently accepted name, plus others
for synonyms and common names. The taxon_meaning_id field contains an ID that is unique
for each species concept within the list so can be used to easily locate and translate
between the different names available for a taxon.

Here's an example which grabs the taxon names in a list with common names:

.. code-block:: sql

  select t.taxon, string_agg(distinct tc.taxon, ', ') as common
  from taxa_taxon_lists ttl
  join taxa t on t.id=ttl.taxon_id
  left join (taxa_taxon_lists ttlc
    join taxa tc on tc.id=ttlc.taxon_id and tc.deleted=false
    join languages lc on lc.id=tc.language_id and lc.iso<>'lat'
  ) on ttlc.taxon_meaning_id=ttl.taxon_meaning_id
  where ttl.deleted=false
  and ttl.taxon_list_id=1
  and ttl.preferred=true
  group by t.taxon

Don't worry if that query is looking a bit complex, later we'll see how the reporting cache
tables make querying both observational and taxonomic data much simpler.

.. tip::

  The taxa.external_key field is often used to store an externally recognised identifier
  for the taxon. In the UK it is used to store the preferred Taxon Version Key as used
  by the NBN.

taxon_groups
------------

The taxon_groups table provides a list of labels (sometimes called reporting categories)
which are often used in reporting to  help clarify taxon names in a user friendly way. Each
taxon belongs to a single taxon group and group names can be taxonomic but don't have to
be, for example a taxon group could  be called "aquatic insects" if desired.

Cache tables
============

The Indicia data model is normalised, which means that data are split across multiple
tables with relationships between the records, as opposed to a more flat "spreadsheet"
approach where there a large number of columns in a single table. This is efficient in
terms of storage and efficiency of updates and it also ensures the integrity of data since
each data value is only stored once. However it can make queries more complex with multiple
joins required to bring in all the tables required for the output of a query and in some
cases the additional joins required can reduce the performance of queries.

In order to make queries easier to write and also performant, Indicia includes a
set of tables which "flatten" the multiple tables of key parts of the data model into
a few tables which are easy to query and, more importantly, perform well when used to
generate report outputs.

cache_occurrences_functional
----------------------------

This table contains all the fields which have a common functional use in building reports
that output occurrence data. This means it includes fields that are used for filtering,
sorting and grouping the report output rather than the labels which are typically output
in the report columns displayed to the user.

.. note::

  By keeping all the commonly filtered, sorted and grouped columns in a single table, the
  PostgreSQL query optimiser is able to effectively perform all the processing on a single
  table then join in other columns to obtain output values for display as a last step. This
  is much more efficient than filtering 2 separate tables then joining to obtain the
  intersection. For example, a query that shows all taxa in the 'insects - beetles' group
  for the Dorset vice county should first obtain the IDs matching the 'insects - beetles'
  taxon group and the Dorset location, then select data from cache_occurrences_functional
  filtering on taxon_group_id and location_id_vice_county within the same table. This is
  MUCH more efficient than joining to the taxon_groups and locations tables to filter
  within those tables.

cache_occurrences_nonfunctional
-------------------------------

Contains additional values for each record which are frequently useful to construct the
display output of a record but rarely used in filtering, grouping or sorting of the report
output.

cache_samples_functional
------------------------

Similar to the cache_occurrences_functional, contains the commonly filtered, sorted and
grouped values for a sample. Note that when querying occurrences this table is unnecessary
since all the values are duplicated in cache_occurrences_functional (for the performance
reasons described above). It is only necessary to use this table when querying a list
of samples.

cache_samples_nonfunctional
---------------------------

Contains additional values for each sample which are frequently useful to construct the
display output of a sample or the sample elements of a record but rarely used in filtering,
grouping or sorting of the report output.

cache_taxa_taxon_lists
----------------------

Contains values pertaining to a single taxon name, for example you can find the used name,
the preferred name for the taxon as well as the default common name, kingdom, order and
family.

cache_taxon_searchterms
-----------------------

A table containing all variants and codes that can be used to lookup a taxon in a single
indexed list.

The following example shows how the cache_* tables can be joined to include all the cached
data relevant to a record. Note that in most cases you won't need to include all the
tables here, just the cache_occurrences_functional table plus any others required in the
output:

.. code-block:: sql

  select
  o.id,
  onf.licence_code,
  snf.public_entered_sref,
  vague_date_to_string(o.date_start, o.date_end, o.date_type),
  cttl.taxon,
  cttl.preferred_taxon as accepted_name,
  cttl.default_common_name as common_name,
  cttl.family_taxon,
  cttl.order_taxon
  from cache_occurrences_functional o
  join cache_occurrences_nonfunctional onf on onf.id=o.id
  join cache_samples_nonfunctional snf on snf.id=o.sample_id
  join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
  where o.taxon_group_id=1
  and o.website_id=2
  and o.survey_id=3

.. tip::

  Because of the way the indexing works on cache_occurrences_functional, if you want to
  filter on a survey_id to restrict the output to a single dataset, also include a filter
  on the website_id as shown in the query above. This allows a compound index to work so
  is much more efficient.

Custom attribute tables
=======================

Indicia is designed to allow flexible capture of wildlife records and to tolerate the fact
that wildlife surveys are often designed with specific attributes in the data, for example
it is possible to record everything from plant abundance on the DAFOR scale or to record
the chemical conditions of seawater in an oceanic sample. Clearly the database model cannot
be designed to cater for all the possible attributes in a traditional way. Instead, the
surveys, samples, occurrences, locations, taxa_taxon_lists and termlists_terms tables
allow allow extension with custom attributes. In the following example, you can replace
<table> with the singular name of the table you are adding a custom attribute to, e.g.
sample_attributes.

<table>_attributes
------------------

For each custom attribute, a record is created in the <table>_attributes table which
describes the global properties of the attribute, including its caption, data type and
validation rules.

<table>_attributes_websites
---------------------------

Each custom attribute is then linked to the website/survey dataset combinations it is being
used for by a record in <table>_attributes_websites. Note that this record can specify
additional validation rules to apply to the attribute within the context of this survey
dataset, for example it is normally appropriate to set an attribute to required in some
survey datasets but not others.

<table>_attribute_values
------------------------

Once a custom attribute has been created for a dataset, the captured values are stored in
the <table>_attribute_values table, which links the <table>_attributes attribute
definition to the actual record in <table>.

By means of illustration, the following query pulls out all the custom attribute values for
samples in a given survey dataset:

.. code-block:: sql

  select
    s.id,
    string_agg(
      a.caption || ': ' ||
        coalesce(v.text_value, v.int_value::varchar, v.float_value::varchar, vague_date_to_string(v.date_start_value, v.date_end_value, v.date_type_value)),
      '; ') as values
  from samples s
  join sample_attribute_values v on v.sample_id=s.id and v.deleted=false
  join sample_attributes a on a.id=v.sample_attribute_id and v.deleted=false
  group by s.id

Some attributes will have the system_function field populated in the <table>_attributes
table. This attribute flags up attributes which have a standard meaning that the system
can recognise, for example there might be a variety of attributes which capture the
biotope associated with a sample and they can all be tagged as such. System function
attributes values for occurrences and samples are automatically added to the
cache_occurrences_nonfunctional and cache_samples_nonfunctional tables respectively, for
example:

.. code-block:: sql

  select id, attr_biotope from cache_samples_nonfunctional


Website agreements
==================

By default, when you use the Indicia reporting system to pull out occurrence records having
authenticated your request as coming from a website registered on the warehouse, the
reporting system will automatically filter the response to only include records belonging
to that website, as long as the report is "well-behaved" of course. This might not always
be the desired behaviour, for example on iRecord the reporting system includes the records
captured via a wide variety of apps and website portals as well as those entered directly
into iRecord itself. The website agreements module in the database provides a way to
declare agreements (like contracts) which websites can join and configure how they
contribute or receive records to and from other websites who have joined the same contract.
It is possible to set different permissions for different "tasks", e.g. a website may
contribute records to the iRecord portal for verification purposes but not general
reporting.

In general you don't need to write queries against the website agreement tables directly
since the reporting system automatically builds the correct list of website_ids to filter
against and inserts this into the report query for you.

Location data
=============

Locations and location data deserves a special mention in any overview of the data model.

locations
---------

Any persistent boundary stored in the database is added as a record in the locations table.
The location has traditional fields such as a name and centroid map reference. It also
has geometry fields for the centroid and boundary which are proper spatial objects
that use the PostGIS extensions for PostgreSQL. This means you can use the rich suite of
PostGIS functions in your queries.

Geometry fields are stored in the database using an internal binary format. In order to
make the field format usable by humans you can use the built in PostGIS functions
st_geomfromtext and st_astext, e.g.

.. code-block:: sql

  -- read the boundary_geom of a location in Well Known Text format
  select st_astext(boundary_geom) from locations where id=123;

  -- Create a geometry using a Well Known Text format point string in EPSG:27700 (OSGB
  -- Easting and Northing 1936), then transform it to web_mercator (EPSG:900913) and assign
  -- it to a location boundary.
  update locations
  set boundary_geom=st_transform(
    st_geomfromtext('POINT(461680 189630)', 27700),
    900913
  )
  where id=123;

These functions both work with the Well Known Text format for describing geometry objects.

.. tip::

  You'll often see the st_transform function in Indicia spatial queries. The geometry
  objects are stored internally in web mercator (EPSG:900913) which is compatible with most
  common web mapping providers such as Google, thus avoiding transformations when drawing
  map layers in most situations. However users will often use local coordinate systems
  like OSGB 1936 easting and northings which will need to be transformed if you want to get
  the correct results.

As another example, you could also use the st_intersects function to find occurrences which
intersect a point or polygon:

.. code-block::

  -- Find all occurrences within a 10km buffer of a known point.
  select *
  from cache_occurrences_functional
  where st_intersects(
    o.public_geom,
    st_transform(
      st_buffer(
        st_geomfromtext('POINT(461680 189630)', 27700),
        10000
      ),
      900913
    )
  );


WKT, postGIS functions (st_geomfromtext, st_astext, st_transform, st_buffer, st_intersects, st_touches)

Locations, map squares,

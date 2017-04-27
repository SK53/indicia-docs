Our baseline query
------------------

Indicia includes several methods of reporting on the information it holds but
underpinning most of these is an XML format which defines a report query, the
input parameters and output columns. Once you have got to grips with this format
it becomes possible to integrate the reports into tables, charts, maps and data
downloads, or even to expose the report output to your own code via web
services. Let's start by choosing a fairly simple query then look at the
possibilities available when this query is integrated into the reporting system.
The following query returns all records added to the system in this month:

.. code-block:: sql

  select snf.public_entered_sref, cttl.preferred_taxon, cttl.default_common_name,
      o.date_start, o.date_end, o.date_type
  from cache_occurrences_functional o
  join cache_samples_nonfunctional snf on snf.id=o.sample_Id
  join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
  where o.created_on>now()-'1 month'::interval;

Whilst not being a very impressive query in its own right, let's take a look at
how to turn this into an Indicia report, then to extend the capabilities of the
report to make it quite a bit more powerful.

.. note::

  The query uses a bit of PostgreSQL specific syntax. It provides a
  piece of text ``'1 month'`` followed by a double colon, which tells the
  database that we want to *cast* the text as another type of data, that is, we
  want to convert it. By converting the text into an *interval* PostgreSQL is
  able to understand that this text actually means an interval of time and to be
  able to use it as such. 

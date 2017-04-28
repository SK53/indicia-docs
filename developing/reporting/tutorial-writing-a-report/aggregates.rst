Aggregate functions in reports
------------------------------

Aggregate queries are those containing functions which calculate a value across rows in the
underlying dataset and output the value against a column or set of columns the data are
grouped against. For example, the following fictional query counts the species at each
site:

.. code-block:: sql

  SELECT site_name, count(*)
  FROM site_species_list
  GROUP BY site_name;

You cannot, however, simply add the GROUP BY clause to the end of your query in a report
XML file, since the version of the query which counts the rows in the results (in order
to enable the paginator on the report grid) won't work. The GROUP BY needs to be removed.
The solution is to flag up the columns in your XML file which contain aggregate functions
and let Indicia add the GROUP BY clause for you (it will actually include all the columns
that are NOT aggregate in the GROUP by). You do this by setting the attribute `aggregate`
to "true" on the `<column>` element.

When you create an aggregate report, Indicia will attempt to build the correct count query
for you. However it is often the case that it will need to be prompted which columns to
include in the distinct row count (this can also help with performance). Set the `in_count`
attribute to "true" on the `<column>` element. Here's a modified version of the tutorial
report which groups the data by taxon group and counts the records:

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
      <column name="taxon_group" sql="cttl.taxon_group"
              display="Taxon group" datatype="text" in_count="true"/>
      <column name="count" sql="count(o.*)"
              display="Record count" datatype="integer" aggregate="true"/>
    </columns>
  </report>

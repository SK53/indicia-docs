Reporting cache tables
======================

Sometimes querying against the Indicia data model might require several joins to obtain
the required information, reducing the performance of the query to a level not really
satisfactory on a database server. For example to provide the basic "what, where, when
and who" of a biological record you need something akin to the following SQL:

.. code-block:: sql

  select 
    t.taxon, tg.title as taxon_group,
    s.entered_sref, l.name as location_name,
    s.date_start, s.date_end, s.date_type, 
    who.text_value as recorder
  from occurrences o
  join samples s on s.id=o.sample_id and s.deleted=false
  left join locations l on l.id = s.location_id and l.deleted=false
  join taxa_taxon_lists ttl on ttl.id=o.taxa_taxon_list_id and ttl.deleted=false
  join taxa t on t.id=ttl.taxon_id and t.deleted=false
  join taxon_groups tg on tg.id=t.taxon_group_id
  join sample_attribute_values who on who.sample_id=s.id and who.deleted=false and 
    who.sample_attribute_id=<attribute ID>
    
Splitting the database fields up into lots of tables is known as normalisation and it 
ensures that each piece of information is only held once in the database (essential for
ensuring data consistency). However it can have a negative impact on performance so 
Indicia's cache_builder module takes the approach of creating "flattened" versions of the
data model which make reporting much simpler. Here's an alternative version of the above
query:

.. code-block:: sql

  select
    cttl.taxon, cttl.taxon_group,
    snf.public_entered_sref, o.location_name,
    o.date_start, o.date_end, o.date_type,
    snf.recorders
  from cache_occurrences_functional o
  join cache_samples_nonfunctional snf on snf.id=o.sample_id
  join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
  
Not only are there less joins, but an important point is that the vast majority of fields 
you might want to filter on are in the `cache_occurrences_functional` table. Filtering
in a single table then joining extra tables for addition of the information required for
output fields is much faster than filtering in different tables in PostgreSQL.

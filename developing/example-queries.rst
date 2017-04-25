**********************************
Example queries for report writers
**********************************

The following queries can all be run using a pgAdmin instance connected to your warehouse
database and assume that you have a full list of species populated in taxon list ID 15
(change this value if needed).

Find details of a species by name:

.. code-block:: sql

  select id, taxon_meaning_id, external_key, taxon, preferred_taxon, default_common_name
  from cache_taxa_taxon_lists
  where taxon ilike '7-spot ladybird'
  and taxon_list_id=15

Find details of a species by external key (preferred Taxon Version Key)

.. code-block:: sql

  select id, taxon_meaning_id, external_key, taxon, default_common_name
  from cache_taxa_taxon_lists
  where external_key='NBNSYS0000008324'
  and taxon_list_id=15
  and preferred=true

When filtering against the cache_occurrences_functional table (which is the preferred
approach to filtering species observations) you can use either the taxon_meaning_id,
preferred_taxa_taxon_list_id or external_key field to limit to a species.

Find records of 7-spot ladybirds within a polygon:

.. code-block:: sql

  select o.id,
    cttl.taxon,
    snf.public_entered_sref,
    vague_date_to_string(o.date_start, o.date_end, o.date_type)
  from cache_occurrences_functional o
  join cache_samples_nonfunctional snf on snf.id=o.sample_id
  join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
  where o.taxa_taxon_list_external_key='NBNSYS0000008324'
  and st_intersects(
    o.public_geom,
    st_transform(
      st_geomfromtext(
        'POLYGON((450000 170000,460000 170000,460000 180000,450000 180000,450000 170000))',
        27700),
      900913
    )
  );

Find a list of all species in the same polygon:

.. code-block:: sql

  select distinct cttl.kingdom_taxon, cttl.order_taxon, cttl.family_taxon, cttl.preferred_taxon
  from cache_occurrences_functional o
  join cache_samples_nonfunctional snf on snf.id=o.sample_id
  join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
  where st_intersects(
    o.public_geom,
    st_transform(
      st_geomfromtext('POLYGON((450000 170000,460000 170000,460000 180000,450000 180000,450000 170000))', 27700),
      900913
    )
  )
  order by cttl.kingdom_taxon, cttl.order_taxon, cttl.family_taxon, cttl.preferred_taxon;

Find all species in a vice county, assuming that a layer of vice counties has been
configured in the warehouse spatial index builder module:

.. code-block::

  select o.id,
  cttl.taxon,
  snf.public_entered_sref,
  vague_date_to_string(o.date_start, o.date_end, o.date_type)
  from cache_occurrences_functional o
  join locations l on l.id=o.location_id_vice_county and l.deleted=false
  where l.name='Dorset';

Warehouse Extension Modules
===========================

The warehouse is designed as a lightweight core essential for all biological recording
usages of Indicia, with a set of optional extension modules that each enable a specific
area of functionality. 

Installation
^^^^^^^^^^^^

Modules can be installed on warehouses by editing the
application/config/config.php file using a text editor, then finding the definition of the
$config['modules'] array. Ensure that this contains the following line, replacing 
module_name with the name of the file system folder which contains the module:

.. code-block:: php

  <?php
  ...
  MODPATH.'module_name',
  ...
  ?>

.. todo:: 

  Notes on clearing cache

The modules are listed below.

.. toctree::

  cache-builder
  data-cleaner
  data-cleaner-ancillary-species
  data-cleaner-designated-taxa
  data-cleaner-identification-difficulty
  data-cleaner-location-lookup-attr-list
  data-cleaner-new-species-for-site
  data-cleaner-occurrence-lookup-attr-outside-range
  data-cleaner-period
  data-cleaner-period-within-year
  data-cleaner-sample-attribute-changes-for-site
  data-cleaner-sample-lookup-attr-outside-range
  data-cleaner-sample-number-attr-outside-range
  data-cleaner-sample-time-attr-outside-range
  data-cleaner-species-location-name
  data-cleaner-without-polygon
  indicia-auth
  indicia-setup
  indicia-svc-data
  indicia-svc-import
  indicia-svc-security
  indicia-svc-spatial
  indicia-svc-validation
  individuals-and-associations
  log-browser
  nbn-species-dict-sync
  notify-verifications-and-comments
  people-tidier
  phpUnit
  spatial-index-builder
  sref-channel-islands
  sref-mtb
  sref-osgb
  sref-osie
  sref-utm
  taxon-designations
  taxon-groups-taxon-lists
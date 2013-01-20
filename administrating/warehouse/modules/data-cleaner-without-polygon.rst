Data Cleaner - Without Polygon Module
-------------------------------------

This module replicates the functionality of the `NBN Record Cleaner WithoutPolygon rule
type
<http://www.nbn.org.uk/Tools-Resources/Recording-Resources/NBN-Record-Cleaner/Creating-verification-rules.aspx>`_. 
It allows the expected distribution range of a species to be specified as a list of grid
squares (hence without a polygon) and flags a notification against records of that
species which fall outside the list of grid squares. For correct configuration in the
warehouse, create a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SpeciesLocationName
* **Error Message** = ...
* **Metadata** ::

    DataFieldName=Species
    DataRecordId=set to the external key (normally the Taxon Version Key) of the species to
    check

* **Other Data** ::

    [grid square size]
    list of grid squares, 1 per line
  
Note that DataFieldName should always be set to Species. The `NBN Record Cleaner 
<http://data.nbn.org.uk/recordcleaner/documentation/NBNRecordCleanerRuleGuide.pdf>`_
supports an additional mode of ViceCounty allowing vice county data to be checked, this is
not currently supported in Indicia.

Under Other Data, specify the grid square size you are using in square brackets, choosing
from one of:

* [10km_GB]
* [10km_Ireland]
* [10km_CI]
* [1km_GB]
* [1km_Ireland]
* [1km_CI]

Each section header should be followed by a list of grid squares one per line. The CI 
square sizes refer to Channel Islands grid data, which is UTM30 on the ED50 datum.

.. note::

  The WithoutPolygon rule type processes each rule after import and converts the list of 
  grid squares into a polygon which it stores in the ``verification_rule.value_geom``
  database field and then uses PostGIS spatial querying to select the species which fall
  outside their range.


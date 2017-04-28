Reporting on spatial fields
===========================

When reporting on the spatial information in a record, you have the following options:

sample entered_sref & entered_sref_system
-----------------------------------------

The text entered by the recorder for the spatial reference is stored in
`sample.entered_sref` and the grid system or projection used is stored in
`sample.entered_sref_system`. The `entered_sref_system` field is either the abbreviation
for one of the supported grid systems (e.g. OSGB, OSIE, MTB) or a numeric EPSG code for an
x, y coordinate system (e.g. 4326 for GPS lat long, 27700 for OSGB Easting Northing).

cache_samples_nonfunctional public_entered_sref & entered_sref_system
---------------------------------------------------------------------

The cache table version of these fields is identical to the version in the samples table
except that for sensitive records or records where site privacy is a concern, the
`public_entered_sref` is nulled so it is safe to show to public users.

cache_occurrences_functional output_sref
----------------------------------------

This field creates a standardised spatial reference string for reporting purposes. The
string is forced to output as British National Grid or Irish Grid format for references
in Great Britain or Ireland respectively. Currently all other locations are output as
latitude and longitude but support could be added for other grid systems as required. The
`output_sref` is also always blurred to take account of sensitivity or privacy blurs or
the accuracy of a record's grid reference or point reference.

samples location_name
---------------------

For records where a free text site or other location name has been provided, the name as
entered is provided in the `sample.location_name` field.

locations table
---------------

For records where a predefined site or other location has been linked to the record, the
locations table record contains the location name, boundary and centroid geometries and
centroid spatial reference. This record can be located using the `sample.location_id`
field.

cache_occurrences_functional location_name
------------------------------------------

For ease of reporting, this field provides either the free text site or other location
name given for a record, or the name of the predefined location linked to the record. It
is automatically obscured if the record is sensitive or private.

samples.geom
------------

The `samples.geom` field contains the spatial object calculated for the entered spatial
reference. It is normally stored as a POLYGON for the grid square or a POINT and uses the
Web Mercator projection EPSG:3857. You can use PostGIS functions to perform various
calculations on the geometry, e.g. `st_centroid(samples.geom)`.

cache_occurrences_functional.public_geom
----------------------------------------

This field is the reporting cache version of `samples.geom`. The only difference is it is
automatically blurred to allow for sensitivity or privacy of the record.

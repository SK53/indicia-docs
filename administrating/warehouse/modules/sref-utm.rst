UTM Spatial References Module
-----------------------------

This module is one of a suite of modules which provide handling of different spatial
reference notation systems, in this case the Universal Transverse Mercator system. Two
variants are supported based on different underlying projections, one being WGS84 / UTM
zone 30N and the other being ED50 / UTM zone 30N. This module is only required on
warehouses which support UTM references for data entry or reporting.

It performs the following tasks:

* Declares the underlying projection's `SRID <http://en.wikipedia.org/wiki/SRID>`_ to be 
  `32630 <http://spatialreference.org/ref/epsg/32630/>`_, which is the numeric code given
  to WGS84 / UTM zone 30N, or to be `23030
  <http://spatialreference.org/ref/epsg/23030/>`_, which is the numeric code given to the
  ED50 / UTM zone 30N.
* Provides a method for checking the format of a provided spatial reference.
* Provides conversions for British National Grid references to and from a polygon in the
  underlying projection.
  
.. tip::

  In order to support additional UTM zones and projections, it is necessary to create
  additional class files in this module's helpers folder. The class should be called by a
  suitable code to store for spatial references of this system and should extend
  **utm_grid**. It should implement a single public static function called get_srid which
  takes no parameters and returns the EPSG code for the UTM grid as looked up on 
  `spatialreference.org <http://spatialreference.org>`_.
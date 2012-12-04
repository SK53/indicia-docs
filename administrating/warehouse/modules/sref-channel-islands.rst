Channel Islands Spatial References Module
-----------------------------------------

This module is one of a suite of modules which provide handling of different spatial
reference notation systems, in this case the UTM30/ED50 grid system as used in the
Channel Islands. It is only required on warehouses which support Channel Islands Grid
references for data entry or reporting. There are two supported variants of this grid, 
one used for Jersey and one for Guernsey which each have a slightly different projection.

It performs the following tasks:

* Declares the underlying projection's `SRID <http://en.wikipedia.org/wiki/SRID>`_ to be 
  `3108 <http://spatialreference.org/ref/epsg/3108/>`_, which is the numeric code given
  to the ETRS89 Guernsey grid, or to be `3109
  <http://spatialreference.org/ref/epsg/3109/>`_, which is the numeric code given to the
  ETRS89 Jersey transverse mercator projection.
* Provides a method for checking the format of a provided spatial reference.
* Provides conversions for Channel Islands grid references to and from a polygon in the
  underlying projection.
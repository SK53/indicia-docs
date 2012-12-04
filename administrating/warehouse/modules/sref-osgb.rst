OSGB Spatial References Module
------------------------------

This module is one of a suite of modules which provide handling of different spatial
reference notation systems, in this case the Ordnance Survey British National Grid system.
It is only required on warehouses which support British National Grid references for data
entry or reporting.

It performs the following tasks:

* Declares the underlying projection's `SRID <http://en.wikipedia.org/wiki/SRID>`_ to be 
  `27700 <http://spatialreference.org/ref/epsg/27700/>`_, which is the numeric code given
  to the OSGB 1936 projection.
* Provides a method for checking the format of a provided spatial reference.
* Provides conversions for British National Grid references to and from a polygon in the
  underlying projection.
MTB Spatial References Module
-----------------------------

This module is one of a suite of modules which provide handling of different spatial
reference notation systems, in this case the German Meßtischblatt system. It is only
required on warehouses which support German MTB Grid references for data entry or
reporting.

It performs the following tasks:

* Declares the underlying projection's `SRID <http://en.wikipedia.org/wiki/SRID>`_ to be 
  `4745 <http://spatialreference.org/ref/epsg/4745/>`_, which is the numeric code given to
  the RD/83 projection.
* Provides a method for checking the format of a provided spatial reference.
* Provides conversions for MTB Grid references to and from a polygon in the underlying 
  projection.
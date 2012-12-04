OSIE Spatial References Module
------------------------------

This module is one of a suite of modules which provide handling of different spatial
reference notation systems, in this case the Irish Grid system. It is only required on
warehouses which support Irish Grid references for data entry or reporting.

It performs the following tasks:

* Declares the underlying projection's `SRID <http://en.wikipedia.org/wiki/SRID>`_ to be 
  `29901 <http://www.dnf.org/registry/coordinate_reference_systems/>`_, which is the 
  numeric code given to the OSNI 1952 projection.
* Provides a method for checking the format of a provided spatial reference.
* Provides conversions for Irish Grid references to and from a polygon in the underlying 
  projection.
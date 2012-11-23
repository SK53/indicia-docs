Quick Species Maps
------------------

The Quick Species Maps prebuilt form provides a simple way of doing distribution maps for
recorded species, with the ability to compare up to 4 species on a single map. A grid
listing recorded species with numbers of available records is shown, plus controls for
easily adding or removing a species from the map.

.. todo:: 

  screenshot

This page type requires `GeoServer <http://geoserver.org>`_ to be set up on the warehouse,
with a layer defined that exposes a list of occurrence records including the species'
external_key (``taxa_taxon_lists.external_key`` field). You will need the name of this
layer layer when you configure the form. If you are the administrator of the warehouse you
are using, then for more information on preparing GeoServer on the warehouse see 
:doc:`../../../administrating/geoserver-setup`. Otherwise please ask your warehouse
administrator for further information on the availability of GeoServer on your warehouse.

.. tip::

  GeoServer is the name of an open source tool which enables access to your records via
  *spatial web services*, in other words it makes it really easy to drop your records onto 
  maps.

To use the Quick Species Maps prebuilt form on an existing Drupal site with the Indicia
forms module installed, simply select **Content > Create content > Indicia pages** from
the admin menu then set the page title, menu and other general settings as you would for
any other Drupal content page. In the **Select Form Category** drop down choose
**Reporting** then **Quick Species Maps**. Click the **Load Settings Form** button to
bring up the Quick Species Maps specific settings. The settings you will need to consider
include:

.. todo::
  
  Link to details of standard settings for reporting and mapping.

* **Feature type for Indicia species layer** - this must be the name of the layer on the 
  GeoServer which will be used to access the records. The name is constructed from the 
  *namespace*, followed by a colon, then the *layer name*. 
* **Field to filter on** - this must be the name of a field exposed in the data for the 
  above layer which contains the taxa_taxon_list.external_key field. This field is often
  used to store a unique identifier for each organism in the dictionary of species held
  within the Indicia warehouse, so records with the same external_key will be the same
  species.
* **SLD files from GeoServer for Indicia species layer** - because this page allows more
  than one species to be added to the map at a time, it is important to specify several
  *styles* which can be automatically cycled through as the species are added to the map,
  ensuring that the species layers can be differentiated. GeoServer uses a standard file
  format (called `SLD <http://www.openspatial.org/standards/sld>`_, or *Styled Layer
  Descriptor*) for defining how map layers are drawn, which can define things like the
  line thickness, fill colour and opacity or symbol to draw as well as to define how the
  appearance changes depending on the data values. This can be used to define the dot size
  according to a data value for example. Because this technology takes place on the server
  rather than on the client it can be a very fast and powerful method of mapping records,
  though the downside is that SLD is a moderately complex file format. However there are a
  handful of default SLDs installed with GeoServer and your warehouse administrator may
  have set up some more for you, e.g. for drawing distribution points in one of several
  colours.

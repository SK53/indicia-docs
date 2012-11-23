Importer
--------

The Importer provides a wizard for importing CSV files into the Indicia 
database. This will typically be occurrence data, but can also be configured to
support locations, species or any other type of information. The Importer prebuilt form
is simply a wrapper for the import_helper class' functionality enabling it to be easily
dropped into a Drupal site if required.

To use the Importer prebuilt form on an existing Drupal site with the Indicia forms module
installed, simply select **Content > Create content > Indicia pages** from the admin menu
then set the page title, menu and other general settings as you would for any other Drupal
content page. In the **Select Form Category** drop down choose **Utilities** then
**Importer**. Click the **Load Settings Form** button to bring up the Importer specific
settings. The settings you will need to consider include:

* **View access control** and **Permission name for view access control** - as described
  under :doc:`generic-settings`.
  
* **Type of data to import** - Select whether you want to set up an import for occurrences
  (= biological records) or locations. There is a third option, to use a setting provided
  in the page URL as a **type** parameter. For example you would need to append 
  ``&type=occurrence`` to the page URL to dictate that the import wizard will allow import
  of occurrence records. In this instance the type parameter must be set to the singular
  name of the database entity you want to import into. Suitable options include:
  
    * occurrence
    * location
    * termlists_term (for term lookup entries)
    * taxa_taxon_list (for species data)
    
  Its quite unlikely that you will need to import the latter 2 types of data from a client
  Drupal website, but possible nonetheless.
* **Preset Settings** - this setting allows you define preset, or default, values that 
  will apply to every single record that is imported. For example, if you were to set up
  an import page for a 24 hour bioblitz at a known site then it might be perfectly valid
  to define the following preset settings, which simplifies the columns that are then
  required in each and every uploaded CSV file::
  
    sample:date=14/08/2012
    sample:location_name=Badbury Rings
    sample:entered_sref_system=OSGB
    
  The last of these 3 settings ensures that all spatial references are imported as British
  National Grid references. Each setting must be provided as the singular version of the
  database entity name followed by a colon then the field name that you are importing data
  into. Note that the **date** field is a special field created to make it simple to set
  data into the **samples** table's date_start, date_end and date_type fields which are
  required for allowing vague dates to be stored,

More information on the import process in general can be found in the
:doc:`../../../administrating/importing` documentation.


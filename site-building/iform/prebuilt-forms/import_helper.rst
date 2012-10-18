Import Helper
-------------

The Import Helper provides a wizard for importing CSV files into the Indicia 
database. This will typically be occurrence data, but can also be configured to
support locations, species or any other type of information.

Column -> database attribute mappings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A significant part of the effort required to import a CSV file is the correct
mapping of columns in the import file to database attributes. The Import Helper
supports remembering of the mappings from a previous import so that, for 
example, if the user maps a "Place" import column to the Sample Location Name
database attribute, future imports of the same import file template will 
remember the mapping so not require user input. In order for this to work, 
the Drupal Profile module must be enabled and a Profile field must be created
to support the capturing of the remembered mappings. To do this:

#. Visit the *Site building > Modules* page in your Drupal installation and 
   check that the *Profile* module is enabled. Enable it if not.
#. Select the *User management > Profiles* menu item. Click *multi-line 
   textfield* in the *Add new field* section.
#. Set the following options:

   * Category=System
   * Title=Import field mappings
   * Form name=profile_import_field_mappings
   * Visibility=Hidden profile field

#. Now save the profile field.

Note that although this profile field will appear under the user's Drupal 
account (accessed via My Account if you are using Instant Indicia) on the System
tab, it will only appear for administrative users since the content is not
intended to be human-readable.


Data Cleaner - Ancillary Species Module
---------------------------------------

This module replicates the functionality of the `NBN Record Cleaner AncillarySpecies rule 
type <http://www.nbn.org.uk/Tools-Resources/Recording-Resources/NBN-Record-Cleaner/Creating-verification-rules.aspx>`_.
It allows a warning to be tagged against records where the species is not in a provided 
list or where the species is in a provided list. The latter is likely to be only 
appropriate for surveys which have a small target list of species. For correct
configuration in the warehouse, create a new verification rule with the following 
settings:

* **Title** and **Description** set as required.
* **Test Type** = AncillarySpecies
* **Error Message** = This species requires|does not require additional checks
* **Reverse Rule** - tick this box if you want to report records where the species is
  in the provided list of species, rather than not in the list of species.
* **Metadata** = 
  SurveyId=n
* **Other Data** =
  ...
  
In the metadata, replace *n* with the survey ID. In the other data section, provide a list
of species names under the heading [Taxa], or species taxon version keys under the heading
[Data]. Note that the latter requires the external_key field of each species on the 
warehouse to be loaded with the preferred taxon version key of the taxon.

.. todo:: 

  Notes on the use of INI to set messages.
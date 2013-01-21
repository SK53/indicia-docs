Data Cleaner - Species Location Name Module
-------------------------------------------

Allows declaration of a rule that tags a verification notification message against any
records of a species that belong to a sample where the location name is not in a list of
allowed location names for the survey. An example usage might be where a species is only
known at a small number of sites. For correct configuration in the warehouse, create a
new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SpeciesLocationName
* **Error Message** = ...
* **Metadata** ::

    SurveyId=ID of the survey being checked
    LocationNames=List of allowed location names, comma separated
    Tvk=External key (normally the preferred taxon version key) of the species
    Taxon=Preferred taxon name
    TaxonMeaningId=Meaning ID from the database for the species
  
Note that you only need to supply one of the Tvk, Taxon or TaxonMeaningId settings in 
order to identify
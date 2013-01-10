Data Cleaner - Species Location Module
--------------------------------------

Allows declaration of a rule that tags a verification notification message against any
records of a species that belong to a sample where the location is not in a list of
allowed known locations for the species/survey combination. An example usage might be
where a species is only known at a small number of sites. For correct configuration in the
warehouse, create a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SpeciesLocation
* **Error Message** = ...
* **Metadata** ::

    SurveyId=ID of the survey being checked
    LocationNames=List of allowed locations' names, comma separated
    Tvk=External key (normally the preferred taxon version key) of the species
    Taxon=Preferred taxon name
    TaxonMeaningId=Meaning ID from the database for the species
  
Note that you only need to supply one of the Tvk, Taxon or TaxonMeaningId settings in 
order to identify
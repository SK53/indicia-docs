Data Cleaner - New Species for Site module
------------------------------------------

This is an Indicia specific extension to the rules supported by the :doc`data-cleaner`. 
It scans the incoming records for a specified survey and looks for any records at a site
where the species has not been previously recorded at that site. For correct configuration
in the warehouse, create a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = NewSpeciesForSite
* **Error Message** = Species not previously recorded at this site
* **Metadata** = SurveyId=n

For the latter, replace *n* with the ID of the survey you want to scan.
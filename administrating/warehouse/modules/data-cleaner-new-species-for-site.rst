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

.. note::

  Because this rule requires the location_id to be filled in to detect the location for a
  record, the survey's data input form must capture a location as well as a grid 
  reference. This rule does not use a spatial query to work out the location for each 
  record, so the rule is only really appropriate for surveys which capture records against
  a defined list of sites.
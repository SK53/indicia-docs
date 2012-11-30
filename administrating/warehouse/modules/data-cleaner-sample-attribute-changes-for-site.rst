Data Cleaner - Sample Attribute Changes for Site Module
-------------------------------------------------------

This is an Indicia specific extension to the rules supported by the :doc`data-cleaner`. It
scans the incoming records for a specified survey and looks for any records at a site
where a certain sample attribute's value changes. This may be useful if a sample attribute
records something that should be persistent at the site but where the recorder of a sample
notes a change to that attribute's value which should be investigated. An example might be
a change to a "site type" attribute. For correct configuration in the warehouse, create a
new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SampleAttributeChangesForSite
* **Error Message** = ...
* **Metadata** = 
  SurveyId=n
  SampleAttr=m

Fill in an appropriate error message and for the latter, replace *n* with the ID of the
survey you want to scan and *m* with the ID of the attribute you want to check doesn't
change.

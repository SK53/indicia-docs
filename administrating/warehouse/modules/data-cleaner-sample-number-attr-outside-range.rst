Data Cleaner Sample Number Attribute Outside Range Module
---------------------------------------------------------

This Data Cleaner module can be configured to provide a notification when a numeric
attribute's value associated with a sample is outside a given range. An example usage of
this would be to allow recording of flying insects (e.g. butterflies) in different wind
conditions using the numeric Beaufort scale but to flag records above force 3 for 
additional checking. For correct configuration in the warehouse, create a new verification 
rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SampleLookupAttrOutsideRange
* **Error Message** = ...
* **Other Data** = ::

  SurveyId=...
  Attr=...
  Low=...
  High=...
  
Set SurveyId to the ID of the survey being checked, set Attr to the ID of the sample
attribute being checked, set Low to the lowest acceptable number and High to the highest
acceptable number. Either Low or High may be omitted. 

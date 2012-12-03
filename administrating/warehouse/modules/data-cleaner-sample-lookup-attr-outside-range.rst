Data Cleaner - Sample Lookup Attribute Outside Range Module
-----------------------------------------------------------

This Data Cleaner module can be configured to provide a notification when a lookup
attribute's value associated with a sample is outside a given range. An example usage of
this would be to allow recording of flying insects (e.g. butterflies) in different wind
conditions but to flag records in non-calm conditions for additional checking. The sort
order of the terms in the termlist linked to the attribute is used to define the limits
of the allowed range. For correct configuration in the warehouse, create a new
verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SampleLookupAttrOutsideRange
* **Error Message** = ...
* **Other Data** = ::

  SurveyId=...
  Attr=...
  JoinMethod=meaning_id or termlists_term_id
  Low=...
  High=...
  
JoinMethod can be omitted in most circumstances but when a survey stores the meaning ID
of a selected term rather than the termlists_term_id this can be used to change how the 
rule links to the terms. Set SurveyId to the ID of the survey being checked, set Attr to
the ID of the sample attribute being checked, set Low to the sort order of the lowest
acceptable term and High to the sort order of the highest acceptable term value. Either
Low or High may be omitted. 

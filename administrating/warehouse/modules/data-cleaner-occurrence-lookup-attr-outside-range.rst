Data Cleaner - Occurrence Lookup Attribute Outside Range Module
---------------------------------------------------------------

This Data Cleaner module can be configured to provide a notification when a lookup
attribute's value associated with a record is outside a given range. An example usage of
this would be for a count attribute which uses a termlist to provide the following range
options:

* 1
* 2-5
* 6-10
* 10+

Whilst the user is free to select any of these options, there is a low likelihood of
more than 10 being counted so this rule type can flag such records for additional
checks. The sort order of the terms in the termlist linked to the attribute is used to
define the limits of the allowed range. For correct configuration in the warehouse,
create a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = OccurrenceLookupAttrOutsideRange
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
the ID of the occurrence attribute being checked, set Low to the sort order of the lowest
acceptable term and High to the sort order of the highest acceptable term value. Either
Low or High may be omitted. 
Data Cleaner - Sample Time Attribute Outside Range Module
---------------------------------------------------------

The Sample Time Attribute Outside Range module allows verification notifications to be
attached to records where a text attribute in format hh:mm is outside a given time
range, or a range of times given in a start and end time custom attribute fall at least
partly outside a given time range. An example might be for a survey that follows a set
methodology where the recording is supposed to occur within a certain period of the day.
Records outside this time of day can be accepted into the system but flagged for
additional checking. For correct configuration in the warehouse, create a new
verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = SampleLookupAttrOutsideRange
* **Error Message** = ...
* **Metadata** ::

  SurveyId=...
  StartTime=...
  EndTime=...
  StartTimeAttr=
  EndTimeAttr=
  
Set SurveyId to the ID of the survey being checked. Set StartTime and EndTime to the start
and end of the time range, in hh:mm format. Set StartTimeAttr and EndTimeAttr to the IDs
of the start and end time custom sample attributes that hold the data being checked. If
you are only recording a single time point for each sample rather than a start and end
time, set both StartTimeAttr and EndTimeAttr to the same custom sample attribute's ID.
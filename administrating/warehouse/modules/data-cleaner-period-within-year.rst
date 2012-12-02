Data Cleaner Period Within Year Module
--------------------------------------

This module replicates the functionality of the `NBN Record Cleaner PeriodWithYear rule 
type <http://www.nbn.org.uk/Tools-Resources/Recording-Resources/NBN-Record-Cleaner/Creating-verification-rules.aspx>`_.
It allows a warning to be tagged against records where the species is recorded oustide a
given time of year, or can be reversed so that the warning occurs when the record is within
the time of year. A typical use of this rule might be to provide a notification for a
record of a species which has a reasonably reliable migration pattern so is only present
in the country for part of the year. For correct configuration in the warehouse, create
a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = PeriodWithinYear
* **Error Message** = ...
* **Reverse Rule** - tick this box if you want to report records of a species which are in
  a date range rather than not in a date range.
* **Metadata** = ::

  StartDate=start of the date range in mmdd format
  EndDate=end of the date range in mmdd format
  Tvk=External key (normally the preferred taxon version key) of the species
  Taxon=Preferred taxon name
  TaxonMeaningId=Meaning ID from the database for the species
  DataFieldName=...
  
Note that you only need to supply a Tvk, Taxon or TaxonMeaningId setting to identify the 
species. ``DataFieldName`` is provided for compatibility with the NBN Record Cleaner rule
files but is not actually used, instead Indicia uses an occurrence attribute with the 
system function option set to 'sex_stage' to determine which attribute identifies the 
stage of the record.
Data Cleaner Period Module
--------------------------

This module replicates the functionality of the `NBN Record Cleaner Period rule type 
<http://www.nbn.org.uk/Tools-Resources/Recording-Resources/NBN-Record-Cleaner/Creating-verification-rules.aspx>`_.
It allows a warning to be tagged against records where the species is recorded oustide a
given date range, or can be reversed so that the warning occurs when the record is within
the date range. A typical use of this rule might be to provide a notification for a record
of a species which arrived in the country on a known date. For correct configuration in
the warehouse, create a new verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = Period
* **Error Message** = ...
* **Reverse Rule** - tick this box if you want to report records of a species which are in
  a date range rather than not in a date range.
* **Metadata** = ::

  StartDate=start of the date range in hhhhmmdd format.
  EndDate=end of the date range in hhhhmmdd format
  Tvk=External key (normally the preferred taxon version key) of the species
  Taxon=Preferred taxon name
  TaxonMeaningId=Meaning ID from the database for the species
  
Note that you only need to supply a Tvk, Taxon or TaxonMeaningId setting to identify the 
species.
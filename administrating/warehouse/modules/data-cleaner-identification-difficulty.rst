Data Cleaner - Identification Difficulty Module
-----------------------------------------------

This module replicates the functionality of the `NBN Record Cleaner 
IdentificationDifficulty rule type 
<http://www.nbn.org.uk/Tools-Resources/Recording-Resources/NBN-Record-Cleaner/Creating-verification-rules.aspx>`_.
This rule type flags species that are not trivial to identify with a rating from 1 to 5
and the rule also identifies the message for each of those ratings. For some taxonomic
groups, for example, a level's might suggest that a specimen is required but this may not
be appropriate for other groups. A single rule can configure the identification difficulty 
for a list of taxa. For correct configuration in the warehouse, create a new
verification rule with the following settings:

* **Title** and **Description** set as required.
* **Test Type** = IdentificationDifficulty
* **Error Message** = ...
* **Other Data** = ::

  [Data]
  list of external keys (e.g. taxon version keys), one per line. Each key is followed by 
  an = then the message ID (a number from one to five)
  [Taxa]
  list of preferred taxon names as an alternative to the Data section. Each key is 
  followed by an = then the message ID (a number from one to five)
  [Ini]
  1=*message for difficulty rating 1*
  2=*message for difficulty rating 2*
  3=*message for difficulty rating 3*
  4=*message for difficulty rating 4*
  5=*message for difficulty rating 5*

So, a rule's Other Data section will contain a Data section and an Ini section, or a Taxa
section and an Ini section, depending on whether the taxa are being listed by external
key or preferred name.
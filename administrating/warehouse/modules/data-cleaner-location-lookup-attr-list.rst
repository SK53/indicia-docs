Data Cleaner - Location Lookup Attribute in List
------------------------------------------------

This is an Indicia specific extension to the rules supported by the :doc`data-cleaner`. It
scans the incoming records for a specified survey and looks for any records at a linked
site where the site has an associated attribute which is either a member of or not a
member of a list of chosen terms. For example you might set up a rule for a bat roost
which tags a warning against all records where the site type is not typical of bat roosts.
For correct configuration in the warehouse, create a new verification rule with the
following settings:

* **Title** and **Description** set as required.
* **Test Type** = LocationLookupAttrList
* **Error Message** = Records for this site type must be checked
* **Reverse Rule** - tick this box if you want to report records where the site type is
  in the list of terms, rather than not in the list of terms.
* **Metadata** = ::
  
    SurveyId=n
    Attr=m
    JoinMethod=meaning_id
    
* **Other Data** = ::
    
    [Terms]
    followed by a list of terms, one per line...
  
In the metadata, replace *n* with the survey ID and *m* with the ID of the location 
attribute you want to check. You only need to set the JoinMethod option to meaning_id when
your survey stores the meaning_id of the term rather than the termlists_term_id in the
attribute's int_value field - most surveys do not do this so if you aren't sure then 
leave this setting out.

.. note::

  Because this rule requires the location_id to be filled in to detect the location for a
  record, the survey's data input form must capture a location as well as a grid 
  reference. This rule does not use a spatial query to work out the location for each 
  record, so the rule is only really appropriate for surveys which capture records against
  a defined list of sites.
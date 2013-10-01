Dynamic weekly counts
---------------------

This form allows you to configure a data entry system for a grid of weekly counts. Each
row represents a species and each column a week during a recording season, with count
numbers being input into the grid cells. The grid can be combined with other dynamically
generated controls as it is an extension of the :doc:`dynamic-sample-occurrence` form.

Typically you might set this form up with a grid of the survey sites and links to the 
input forms for each season. The following steps describe how you might set this up.

  #. In the warehouse, create a term in the location types termlist to identify the list
     of sites you are using (e.g. "weekly counts site") and create at least one site 
     that has this location type.
  #. Also in the warehouse create a survey to capture your records. Associate a single 
     occurrence attribute called "Count" of type integer with your survey.
  #. Finally for the warehouse setup, create a species list and import the list of species
     you want to record against.
  #. Next, in your Drupal site create a new IForm page using the **Reporting > Dynamic 
     Report Explorer** page type. 
  #. Set **Report settings > Report name** to ``Reports for prebuilt forms\Weekly 
     Counts\Sites and weekly counts list``.
  #. Set the **Report settings > Preset parameters** to contain the following:
  
       location_type_id=...
       
     Replace the ... with the ID of the term you created in the location types termlist.
  #. In the **Report settings > Columns configuration**, click on the **Edit source**
     option then paste the following into the box:
     
     .. code-block:: json
     
       [
         {
           "fieldname":"name",
           "display":"Site name"
         },
         {
           "fieldname":"last_year",
           "template":"<a href='{rootFolder}weekly-count-input&sample_id={sample_id_last}&location_id={id}&year={last_year}' 
           class='exists-{last_yr_exists}' title='Edit weekly counts for {last_year} at {name}'>{last_year}</a>",
           "display":"Last year"
         },
         {
           "fieldname":"this_year",
           "template":"<a href='{rootFolder}weekly-count-inputs&sample_id={sample_id_this}&location_id={id}&year={this_year}' 
           class='exists-{this_yr_exists}' title='Edit weekly counts for {this_year} at {name}'>{this_year}</a>",
           "display":"This year"
         }
       ]
       
     In the href attributes, you will need to replace "weekly-count-input" with the path 
     to the form you are about to create for recording weekly counts if you choose to give 
     it a different URL alias. Also note that if you are using clean URLs in Drupal, 
     replace the ``&`` immediately following this with a ``?``.
  #. Now set up the Drupal menu settings if you want this page to appear on the menu and
     save the page.
  #. Create another IForm page, this time using the **General Purpose Data Entry Forms > 
     Weekly counts** form.
  #. Set the **URL path settings** option to ``weekly-count-input``, or whatever value you
     used in the links you created earlier.
  #. Click **Load Settings Form**. In the **Other IForm Parameters** section, select
     the **Survey** you created earlier in the warehouse.
  #. Also in the **Other IForm Parameters** section, set **Redirect to page after 
     successful data entry** to the path of the page you created with the sites report
     on.
  #. Set **User Interface > Interface Style Option** to **All One Page**.
  #. Under **User Interface > Form Structure**, paste the following::
     
       =Counts=
       [location url param]
       [*]
       [weekly counts grid]
       
     The ``[location url param]`` control defines that the location ID will be supplied
     as a URL parameter (provided by the report grid link).
  #. Under **Species**, set the **Species List** to the list you created earlier.
  
Save your page. Now return to the sites list page and click on one of the year links to 
start testing data entry. 

.. tip::

  The report grid we configured earlier attaches a CSS class to each link, called either
  ``exists-yes`` or ``exists-no``. You can use these to easily style the links to existing
  sets of data differently to those which have not been input yet.
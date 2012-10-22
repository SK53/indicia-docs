Butterfly Transect Walks Example Setup
--------------------------------------

Indicia includes a prebuilt form designed for inputting flying insect counts 
along a transect walk which has been divided into sections. This form was 
designed for the `UKBMS <http://www.ukbms.org/>`_'s online recording facilities
but can also be used to record other flying insects such as Odonata.

Some details on how you might set this form up follow, including the setup of 
a calendar grid to break walks down into weeks through the season. Before 
following these steps you will need an installation of Instant Indicia (or 
Drupal plus the Indicia Forms module if you are also able to setup features
such as Easy Login) as well as an account on a warehouse.

Here are some files you may like to have available to import into the system:

+------------+-----------------------------------------------------------------+
| File       | Description                                                     |
+============+=================================================================+
| Counties   | If not using the list of counties provided on the warehouse then|
| CSV        | provide a list of the counties that sites will be allocated to. |
|            | This should be provided as a CSV file with a single column      |
|            | containing the county names, including a column title (which can|
|            | be anything you like).                                          |
+------------+-----------------------------------------------------------------+
| Habitats   | Provide a list of the habitats that will be available for       |
| CSV        | describing sites in your recording scheme.                      |
|            | This should be provided as a CSV file with a single column      |
|            | containing the county names, including a column title (which can|
|            | be anything you like). If available, a sort order column        |
|            | containing an integer for each term can be used to enforce a    |
|            | non-alphabetical sort order.                                    |
+------------+-----------------------------------------------------------------+
| Management | Provide a list of the management terms that will be available   |
| CSV        | for describing sites in your recording scheme.                  |
|            | This should be provided as a CSV file with a single column      |
|            | containing the county names, including a column title (which can|
|            | be anything you like).                                          |
+------------+-----------------------------------------------------------------+
| Branches   | This file is only required if your recording scheme is divided  |
| CSV        | into regional branches. An ESRI SHP file format list of the     |
|            | boundaries of each branch, containing the branch names and the  |
|            | polygon defined in projection EPSG:27700 or EPSG:4326.          |
+------------+-----------------------------------------------------------------+
| Transects  | If you want to prepopulate the list of sites available for      |
| CSV        | transect walks, then provide a list of the transects as a       |
|            | spreadsheet in CSV format, including column titles. The         |
|            | spreadsheet should include the following columns:               |
|            |                                                                 |
|            | * **Site code**. Provide a unique numeric code for each site.   |
|            | * **Site name**. Provide a name for each site.                  |
|            | * **Grid ref**. Grid reference for each site's centroid.        |
|            | * **County**. Name of the county for each site. This must match |
|            |   one of the counties in the Counties CSV file.                 |
|            | * **Number of sections**. The number of sections the transect   |
|            |   is divided into. If this column is ommitted then you will     |
|            |   need to manually set the number of sections and input the     |
|            |   section details before inputting count data.                  |
|            | * **Overall transect length**. The length of the transect in    |
|            |   metres, can be omitted if not known.                          |
|            | * **Transect width**. The width of the transect in metres, can  |
|            |   be omitted if not known. You will need to know the distinct   |
|            |   list of widths in use so that you can later set up the        |
|            |   appropriate entries for the list of available widths.         |
|            | * **Year established**. Specify the 4 digit year each transect  |
|            |   was established if known.                                     |
|            | * **All or single species**. A column containing the word *All* |
|            |   or *Single* for each transect, depending on the transect type.|
|            | * **Sensitive**. A column containing *t* for sensitive sites    |
|            |   and *f* for all others.                                       |
|            | * **Primary habitat**. Set to one of the terms from the list of |
|            |   habitats where the primary habitat is known.                  |
|            | * **Secondary habitat**. Set to one of the terms from the list  |
|            |   of habitats where the primary habitat is known.               |
|            |                                                                 |
|            | The exact column titles you use does not matter as long as you  |
|            | remember which is which.                                        |
+------------+-----------------------------------------------------------------+
| Sections   | If you want to prepopulate the list of sites available for      |
| CSV        | transect walks, then provide a list of the transects as a       |
|            | spreadsheet in CSV format, including column titles. The         |
|            | spreadsheet should include the following columns:               |
|            |                                                                 |
|            | * **Grid ref** (if not importing a SHP file). This can be the   |
|            |   same as the grid reference for the parent transect but the    |
|            |   recorders will need to draw their routes on a map before      |
|            |   inputting records.                                            |
+------------+-----------------------------------------------------------------+
| Sections   | An ESRI SHP file of the section lines                           |
| SHP        |                                                                 |
+------------+-----------------------------------------------------------------+
| Species    | A CSV file of each of the species you would like to be able to  |
| CSV        | record. Should have a column for the latin name plus a column   |
|            | for the common name, plus one column for any species code       |
|            | systems you would like to be able to use, e.g. BRC codes.       |
|            | You can provide additional species lists if you want to be able |
|            | to record additional species groups via additional tabs.        |
+------------+-----------------------------------------------------------------+

Website registration and survey
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As with any Indicia based survey, you will need a website registration on the 
warehouse plus an entry in the list of surveys, belonging to the website.
Give your survey a name that you will remember as being associated with the
butterfly transect walk survey you are configuring.

Termlists
^^^^^^^^^

Before setting up the form, you will need to have certain terms and termlists
configured on the warehouse as follows. All the termlists you create should be
owned by your website registration on the warehouse.

* Ensure that the existing Location Types termlist includes terms called
  **Branch**, **Transect** and **Transect Section**. Create them if they don't
  already exist. 
* If not using the existing list of counties, then create a termlist called 
  **BMS Counties** or similar. Use the warehouse import tool to import the CSV 
  file of counties into the list, setting the language to English for all rows
  and mapping your column to the **term** field.
* Create a termlist called **Transect width (m)** and setup terms called **5**,
  **6**, **10** and **other**, with the Sort Order set to **5**, **6**, **10** 
  and **9999** respectively. You can modify this list if your scheme has a
  different set of possible transect widths. 
* Create a termlist called **All or single species** with terms for **All** and
  **Single**. Set both terms to English language, with their sort order set to
  **0** and **1** respectively.
* Create a termlist called **Climate of transect** with terms for **Lowland** 
  and **Upland**. Set both terms to English language, with their sort order set
  to **0** and **1** respectively.
* Create a termlist called **BMS Habitats** or similar. Use the warehouse import
  tool to import the CSV file of habitats into the list, setting the language to
  English for all rows and mapping your column to the **term** field. Also
  import the sort order if provided to ensure the habitats are in the correct 
  order.
* Create a termlist called **BMS Management**. Use the warehouse import tool to
  import the CSV file of management terms into the list, setting the language to
  English for all rows and mapping your column to the **term** field.

Species Lists
^^^^^^^^^^^^^
.. todo::
  
  Custom attributes & remaining setup


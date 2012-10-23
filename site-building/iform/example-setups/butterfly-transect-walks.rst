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
| Wind Speed | A CSV file of each of the wind speed terms you would like to be |
| CSV        | able to record.                                                 |
+------------+-----------------------------------------------------------------+
| Wind Dir   | A CSV file of each of the wind direction terms you would like   |
| CSV        | to be able to record.                                           |
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
* Create a termlist called **BMS Wind Speeds**. Use the warehouse import tool to
  import the CSV file of wind speed terms into the list, setting the language to
  English for all rows and mapping your column to the **term** field.
* Create a termlist called **BMS Wind Directions**. Use the warehouse import 
  tool to import the CSV file of wind direction terms into the list, setting the 
  language to English for all rows and mapping your column to the **term** 
  field.
* Create a termlist called **BMS Temperatures**. Use the warehouse import tool 
  to import the CSV file of temperature terms into the list, setting the 
  language to English for all rows and mapping your column to the **term** 
  field.

Species Lists
^^^^^^^^^^^^^

Before importing the species lists you want to be able to record against, ensure
that the **Taxon Code types** termlist contains a term for any species codes 
that you would like to import alongside the species names, e.g. for BRC codes
or Species ID 2010. You must provide species names in a spreadsheet with the 
following columns, note that the exact column names used does not matter:

* Latin name - the latin name of the species, imported into the **Taxon > 
  Taxon** field.
* Common names - the common name(s) of the species, imported into the **Other 
  Fields > CommonNames** field. Provide as a comma separated list, with the 
  preferred first. You can follow each name by a pipe (|) then the 3 letter ISO 
  639 language code for the language, e.g.::

    Green Woodpecker|eng,Pic vert|fra

  This field can be ommitted if common names are not used.
* Codes - any coding systems for the species such as BRC codes, imported into 
  the **Other Fields > Codes** field. The field can contain several codes 
  separated by a comma. Each code must contain the code name (matching the term 
  in the Taxon Code types termlist), followed by a pipe (|), then the actual 
  code, e.g::

    Species ID 2010|172500,BRC Code|123456

Custom Attributes
^^^^^^^^^^^^^^^^^

Setup the following location attributes for the UKBMS survey. Do not make any of
them required at this stage or link them to the location types as this needs to 
be done after import. The attribute is described as block/sub-block/caption, 
followed by the description of the attribute. For example, you should create
a location attribute called county which is a lookup, linked to the BMS Counties
termlist. On the survey setup attributes you will need to make the attribute
required and linked to the Transect location type, but only after the import
of any existing transects.

* **Site details/Details/County**
  Lookup, BMS Counties termlist, linked to Transect location type, required for 
  the survey.
* **Site details/Details/No. of sections**
  Integer, linked to Transect location type, minimum 0, required for survey
* **Site details/Details/Overall length (m)**
  Integer, linked to Transect location type, minimum 0, required for survey
* **Site details/Details/Transect width (m)**
  Lookup, Transect widths termlist, linked to Transect location type, required 
  for survey
* **Site details/Details/Year established**
  Integer, linked to Transect location type
* **Site details/Details/All or single species**
  Lookup, All or single species termlist, linked to Transect location type
* **Site details/Details/Climate of transect**
  Lookup, Climate of transect termlist, linked to Transect location type
* **Habitat and management/Habitat/Principal transect habitat**
  Lookup, Habitats termlist, linked to Transect location type
* **Habitat and management/Habitat/2nd transect habitat**
  Lookup, Habitats termlist, linked to Transect location type
* **Habitat and management/Habitat/Principal habitat present**
  Lookup, Habitats termlist, linked to Section location type
* **Habitat and management/Habitat/2nd habitat present**
  Lookup, Habitats termlist, linked to Section location type
* **Habitat and management/Habitat/3rd habitat present**
  Lookup, Habitats termlist, linked to Section location type
* **Habitat and management/Habitat/4th habitat present**
  Lookup, Habitats termlist, linked to Section location type
* **Habitat and management/Habitat/Habitat text description**
  Text, linked to Section location type
* **Habitat and management/Habitat/Notes on land use and management**
  Text, not linked to a specific location type
* **Habitat and management/Management/Primary management**
  Lookup, Management termlist, linked to Section location type
* **Habitat and management/Management/Secondary management**
  Lookup, Management termlist, linked to Section location type
* **Habitat and management/Management/Management text description**
  Text, linked to Section location type
* **Section/Details/Section length (m)**
  Integer, minimum 0, linked to Section location type
* **CMS User ID**
  Integer, available to other websites, linked to Transect location type
* **Sensitive**
  Boolean, available to other websites, linked to Transect location type

Setup the following custom attributes for occurrences in your survey:

* **Abundance Count**
  integer, required for the survey, minimum value 0, system function = Count or 
  abundance of a sex or life stage.

Setup the following custom attributes for samples in your survey:

* **Recorder Name**
  Text, system function=full name, sample method=Transect
* **Start Time (hh:mm)**
  Text, regexp=/^([0-1][0-9]|2[0-3]):([0-5][0-9])$/, required for survey, 
  default control type=text_input, sample Method=Transect, available to other
  websites
* **End Time (hh:mm)**
  Text, regexp=/^([0-1][0-9]|2[0-3]):([0-5][0-9])$/, required for survey, 
  default control type=text_input, sample Method=Transect, available to other
  websites
* **% sun**
  Integer, min value=0, max value=100
* **Temp (Deg C)**
  Lookup, BMS Temperatures list, required for survey, sample method=Transect
* **Wind Direction**
  Lookup, BMS Wind Directions list, Default value=Not recorded/no data, default 
  control type=select, sample Method=Transect
* **Wind Speed**
  Lookup, UKBMS Wind Speeds list, required for survey, default control 
  type=select, sample method=Transect
* **CMS User ID**
  Use the existing attribute, Sample Method=Transect. This attribute is not 
  needed if the Easy Login module is enabled.
* **CMS Username**
  Use the existing attribute, Sample Method=Transect. This attribute is not 
  needed if the Easy Login module is enabled.

.. todo::
  
  Remaining setup of forms in Drupal


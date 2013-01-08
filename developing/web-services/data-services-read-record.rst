Data Services - reading a record
================================

Reading a single record from the Data Services follows the :doc:`general principles for
reading data <data-services-reading>`. You simply extend the web service URL for the 
entity you want to read from with the ID of the record you want to read.

Examples
--------

Assuming that your warehouse is installed at www.mywarehouse.com and you have obtained 
:doc:`valid read authentication tokens <authentication-overview>`, the following examples
illustrate how to read records from the Data Services. Service calls are shown with GET
parameters though the parameters can also be sent as POST.

Example 1 - basic attributes of occurrence ID 10 in JSON format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This request uses the default list_occurrences view to return minimal information of a 
record.

Request::

  http://www.mywarehouse.com/index.php/services/data/occurrence/10
  &nonce=<nonce>&auth_token=<auth_token>

Example response:

.. code-block:: json

  [{
    "survey":"Demonstration Survey",
    "location":"Poole",
    "date_start":"1980-01-01",
    "date_end":"1980-12-31",
    "date_type":"Y",
    "entered_sref":"SU012023",
    "entered_sref_system":"osgb",
    "taxon":"White Egret",
    "website_id":"1",
    "id":"10",
    "recorder_names":null,
    "zero_abundance":"f",
    "taxon_list_id":"2"
  }]
  
Example 2 - information on a taxon group, including column and count
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This request uses the **wantColumns** and **wantCount** URL parameters.

Request::

  http://localhost/indicia/index.php/services/data/taxon_group/4
  ?nonce=<nonce>&auth_token=<auth_token>&wantColumns=1&wantCount=1
  
Example response:

.. code-block:: json
  
  {
    "records":[
      {"id":"4","title":"Beetles","website_id":null}
    ],
    "columns":{
      "id":{"type":"int","max":2147483647,"unsigned":false,"null":true},
      "title":{"type":"string","null":true},
      "website_id":{"type":"int","max":2147483647,"unsigned":false,"null":true}
    },
    "count":1
  }
  
Example 3 - detailed attributes of occurrence ID 10 in XML format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This request uses the default list_occurrences view to return minimal information of a 
record.

Request::

  http://www.mywarehouse.com/index.php/services/data/occurrence/10
  &view=detail&mode=xml&nonce=<nonce>&auth_token=<auth_token>

Example response:

.. code-block:: xml

  <?xml version="1.0"?>
  <occurrence xmlns:xlink="http://www.w3.org/1999/xlink">
  <id>10</id>
  <confidential>f</confidential>
  <taxa_taxon_list_id>3</taxa_taxon_list_id>
  <taxon_meaning_id>5</taxon_meaning_id>
  <record_status>C</record_status>
  <taxon>Little Egret</taxon>
  <entered_sref>SU012023</entered_sref>
  <entered_sref_system>osgb</entered_sref_system>
  <geom>--binary geometry data--</geom>
  <wkt>--well known text geometry data</wkt>
  <survey_id>1</survey_id>
  <date_start>1980-01-01</date_start>
  <date_end>1980-12-31</date_end>
  <date_type>Y</date_type>
  <location id="2" xlink:href="http://localhost/indicia/index.php/services/data/location/2">Poole</location>
  <website_id>1</website_id>
  <created_by id="1" xlink:href="http://localhost/indicia/index.php/services/data/user/1">admin</created_by>
  <created_on>2012-02-10 17:41:03</created_on>
  <updated_by id="1" xlink:href="http://localhost/indicia/index.php/services/data/user/1">admin</updated_by>
  <updated_on>2012-02-10 17:41:03</updated_on>
  <downloaded_flag>N</downloaded_flag>
  <sample_id>10</sample_id>
  <deleted>f</deleted>
  <zero_abundance>f</zero_abundance>
  <taxon_list_id>2</taxon_list_id>
  </occurrence>

Reading data via the data services
==================================

Reading data from the Indicia warehouse is performed via a set of web services, the **data
services**. Some basic principles are:

* Requests for data need :doc:`read authentication <authentication-overview>` tokens 
  attached as GET or POST parameters. These tell the warehouse that the request for data
  is authentic and which website is requesting data, so that it can filter the response to
  return appropriate records. 
* The Data Services are accessed via the URL of the site root + /index.php/services/data/ 
  + the name of the required data entity, which is the singular version of the required 
  table name, for example ``http://www.mysite.com/index.php/services/data/termlist``.
* The attributes returned for each record are loaded from database views rather than 
  direct from the table. This gives the chance to return meaningful information for each
  record, for example the **termlists_term** entity is used to load terms from a term
  list, even though the terms themselves are stored in the **term** entity. So, the views
  used by the data services to access the **termlists_terms** table join to the **terms**
  table to include the term in the results set. By default, the view used to load records
  for the data services response is called `list_`` followed by the table name, in this
  case **list_termlists_terms**. The prefix of the table loaded can be overridden by
  specifying a **view** GET or POST parameter, e.g. specifying view=detail will load
  records from ``detail_termlists_terms``.
* Calls to the URLs normally return a formatted JSON document describing the results. 
  Provide a GET or POST parameter called **mode** with one of the following values to 
  override the output format:
  
    * **json** - for JavaScript Object Notation (JSON) format
    * **csv** - for Comma Separated Values file format
    * **nbn** - for a tab delimited file compatible with the NBN Exchange format
    * **xml** - for an XML document format. 
    
* Requests sent to the Data Services return the records only by default. You can also 
  request the specification of the columns returned or the count of records. The following
  URL parameters can be provided via GET or POST to control this:
  
  * **wantRecords** controls whether the records are returned
  * **wantColumns** controls whether the column specifications are returned
  * **wantCount** controls whether the record count is returned (e.g. can be used for
    providing pagination information in a grid). 
    
  If your Data Services request returns only one of the available types of information 
  (records, columns or count), then the required information is returned as the top level
  item in the response. If there are more than one pieces of information requested then 
  the top level of the response will be an array or list of the items, each containing the
  relevant set of records, set of columns or count as a sub-item.
* For cross-site retrieval using **JSONP**, an optional callback method can be specified 
  by providing ?callback=methodname in the GET string.
* Although RESTful standards dictate that the GET request is used to get information
  whereas POST requests are used to post records back, the Data Services support POST as
  well as GET for all parameters. The main reason for this is to support long queries that
  can break the limits of a URL on some browsers and web servers, such as requests which
  include a complex polygon boundary for a spatial query.

.. tip::
  Specific outputs for each entity can be defined by adding views that generate the 
  formatted output to the `modules/indicia_svc_data/views/services/data/<entity name>` 
  folder. The view filename defines the mode you request. For example, there is a view
  in `modules/indicia_svc_data/views/services/data/termlists_term/li.php` which outputs
  terms in HTML `<li>` elements, requested when accessing the termlists_term entity with
  `mode=li` as a parameter.
  
Attaching XSL to XML output
---------------------------

By using mode=xsl and passing a GET parameter called xsl to the URL, an XSL transformation
can be linked to by the returned XML document. Either a fully qualified path to the XSL
document is required, or if just a file name is given then the XSL document must exist in
the folder \media\services\stylesheets within the website root. An example file called
default.xsl is provided. For example
``http://www.mysite.com/index.php/services/data/termlist?xsl=default.xsl`` retrieves the
XML document listing all termlists into the browser and formats it on the client using the
XSL file to appear as an HTML table.

Information on how to read individual records and lists of records in one go are in the
following pages.
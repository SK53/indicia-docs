RESTful web service resources
=============================

For up to date documentation on the available resources, ensure that the rest_api warehouse
module is installed then visit `index.php/services/rest`. Currently the resources available
are limited to those required to support accessing reports as well as those required to
support the [http://indicia-online-recording-rest-api.readthedocs.io/en/latest/
online recording REST API] for exchanging records between online recording systems.

The `taxon-observations` and `annotations` resources are both covered in the
[http://indicia-online-recording-rest-api.readthedocs.io/en/latest/
online recording REST API] documentation.

index.php/services/rest
-----------------------

By visiting the root of the REST API you can access dynamically generated documentation of
the other resources available via the API. This endpoint does not need authentication.

index.php/services/reports
--------------------------

The reports resource provides access to Indicia's reporting system, allowing a variety of
queries to be run against the database with parameters of your choice. The resource can:

  * return the folders and reports within a single level of the reports hierarchy, e.g. by
    calling /reports or /reports/library.
  * return the output of a report, with parameters provided in the URL query string, e.g.
    by calling
    /reports/library/occurrences/filterable_explore_list.xml?verified_date_from=2017-05-22.
  * return the list of columns in a report, e.g. by calling
    /reports/library/occurrences/filterable_explore_list.xml/columns.
  * return the list of parameters for a report, e.g. by calling
    /reports/library/occurrences/filterable_explore_list.xml/params.

index.php/services/taxon-observations
-------------------------------------

Provides access to occurrences stored on the warehouse. Described fully in the
[http://indicia-online-recording-rest-api.readthedocs.io/en/latest/ online recording REST
API] documentation.

index.php/services/annotations
------------------------------

Provides access to occurrence comments stored on the warehouse including verification
decisions. Described fully in the [http://indicia-online-recording-rest-api.readthedocs.io/en/latest/
online recording REST API] documentation.

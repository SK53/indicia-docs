*************************
Installation Requirements
*************************

For the client website, assuming that the website will use the client helpers 
PHP API the requirements are as follows:

* PHP version 5.3 to 5.5 is recommended. If installing onto Drupal 6 then
  use PHP version 5.3.
* The cUrl PHP extension should be enabled.
* Any other requirements of the website (e.g. for running Drupal if using this 
  option).
* Your webserver must not be blocked from accessing the Warehouse server by a 
  firewall to allow communications between the 2 servers.

For the Warehouse, the requirements are as follows:

* PHP version 5.3 to 5.5 is recommended.
* The cUrl PHP extension should be enabled.
* PostgreSQL 8.4 or higher is required. 9.x is recommended.
* The PostGIS extension for PostgreSQL must be installed.
* In addition you might like to consider installing GeoServer alongside the 
  Warehouse to support spatial data. This requires a Java SDK.

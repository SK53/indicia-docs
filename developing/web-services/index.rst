************
Web services
************

Indicia's web services are a key component of the Indicia warehouse, since all
interactions between the client website and the warehouse are via web services. This
approach means there is no practical difference between hosting your client website on
the same machine as the warehouse or hosting it on the other side of the globe. The web
services are effectively a set of functions that can be called remotely, for example
functions which return data, allow addition of records to the warehouse, or perform
utility calculations such as spatial reference transformations where these can't be
handled on the client.

.. tip::

  Indicia now has a growing RESTful web service for reading reports and certain other
  types of data. See :doc:`Indicia's RESTful web services <../rest-web-services/index>`

.. toctree::

  authentication-overview
  authentication-client-helpers
  data-services-reading
  data-services-entity-list
  data-services-taxon-search
  data-services-read-record
  data-services-read-dataset
  data-services-read-client-helpers
  data-services-write
  submission-format
  data-services-write-client-helpers
  web-services-errors
  tutorial-data-services-write
  reporting-services
  user-identifiers
  security-services-details/index
  import-services
  spatial-services
  validation-services
  standalone-code

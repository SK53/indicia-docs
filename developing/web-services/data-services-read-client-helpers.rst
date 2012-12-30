Data Services - reading data using the Client Helpers API
=========================================================

The PHP Client Helpers API provides methods which simplify the use of the Data Services
web services to access records on the warehouse. The **data_entry_helper** class provides
the **get_population_data** method which supports loading of data via entity views or
reports, sorting, filtering and local caching. A full description of the method parameters
is provided in the method's documentation.

.. todo::

  Link to the API documentation.

Example 1 - reading a record using the Client Helpers API in PHP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using the PHP Client Helpers API, the first example's request can be invoked using the
following code:

.. code-block:: php

  <?php
    // This example authenticates against the demonstration website
    $readAuth=data_entry_helper::get_read_auth(1, 'password');
    $records=data_entry_helper::get_population_data(array(
      'table' => 'occurrence',
      'extraParams' => $readAuth + array('id'=>10),
      'nocache' => true // forces a load from the db rather than local cache
    ));
    // $records[0] is now an array holding the record details
  ?>
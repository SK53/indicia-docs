Usage
=====

Introduction
------------

Module has a few usages. The service it provides is access through a few dedicated links using
POST requests.

.. _send-record:
Send a record
-------------

Sending a record is straightforward. The submission service endpoint is at *'mobile/submit'*.
Along with the recording forms input values Appsecret and Appname has to be provided, so that
the module can authenticate your request and proceed the data to the Indicia's warehouse.


.. _user-register:
Register With the website
-------------------------

To register with the website that the module is hosted at, an endpoint of
*'user/mobile/register'* is used.

.. _user-login:
Login
-----

As with registering a new user account, signing in through the module to an existing one
is through the same service endpoint *'user/mobile/register'*.

.. _reports:
Access Warehouse Reports
------------------------

The module allows to retrieve data from associated warehouse using its reports.
The endpoint for this is  *'mobile/report'*.


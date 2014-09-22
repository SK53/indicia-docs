Introduction
============

Mobile Authentication module extends the Indicia's iForm module towards the support of
external applications.

Along with the recording forms input values Appsecret and Appname has to be provided, so that
the module can authenticate your request and proceed the data to the Indicia's warehouse.

Through multiple services it provides :

- :ref:`record submission <send-record>`
- :ref:`warehouse report downloading <reports>`
- :ref:`user authentication <user-login>`
- :ref:`user registration <user-register>`


The services it provides are accessed through a few dedicated links using
POST requests.

.. _send-record:
Send a record
-------------

Sending a record is straightforward. The submission service endpoint is at *'mobile/submit'*.
The minimal POST message fields that need to be provided are:

Warehouse information:

- website_id
- survey_id

Record data:

- sample:date
- sample:entered_sref
- sample:entered_sref_system
- occurrence:taxa_taxon_list_id

Please check the :ref:`example <send-record-example>`.

.. _user-register:
Register With the website
-------------------------

To register with the website that the module is hosted at, an endpoint of
*'user/mobile/register'* is used.

Please check the :ref:`example <user-register-example>`.

.. _user-login:
Login
-----

As with registering a new user account, signing in through the module to an existing one
is through the same service endpoint *'user/mobile/register'*.

Please check the :ref:`example <user-login-example>`.

.. _reports:
Access Warehouse Reports
------------------------

The module allows to retrieve data from associated warehouse using its reports.
The endpoint for this is  *'mobile/report'*.

Please check the :ref:`example <reports-example>`.
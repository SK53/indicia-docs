Introduction
============

Mobile Authentication module extends the Indicia's iForm module towards the support of
external applications. Through multiple services it provides:

- :ref:`send-record`
- :ref:`reports`
- :ref:`user-login`
- :ref:`user-register`

All the services the Mobile Auth module provides are accessed through a few
dedicated links using POST requests.

The main requirement for being able to use the services is the application authorisation,
more specifically - valid Appsecret and Appname has to be setup and provided.
Read more about :ref:`account-management`.

.. note:: Both, this and iFrom modules, could be hosted and configured
  to use specific warehouses on any Drupal site (please read :ref:`setup`),
  but since all the infrastructure is set up on a
  `BRC's iRecord website <http://www.brc.ac.uk/irecord>`_
  all the examples here will be using the iRecord.

.. _send-record:

Sending a record
----------------

There are two types of record submission: *authenticated* and *anonymous*.
Sending an anonymous record is quite straightforward. The submission service endpoint
is at ``'mobile/submit'``. The minimal POST message fields that need to be provided are:

Warehouse information:

- website_id
- survey_id

Record data:

- sample:date
- sample:entered_sref
- sample:entered_sref_system
- occurrence:taxa_taxon_list_id

*Authenticated record* submission adds a requirement: the record should go along with either
iRecord active *session cookie*, which would authenticate the user, or attaching to the record
user's ``usersecret`` along with its ``email``.
The ``usersecret`` can be manually set up and obtained using iRecords web interface by visiting
user account settings ``brc.ac.uk/irecord/user -> Edit -> Indicia mobile auth``
updating ``User shared secret`` field. Or through :ref:`login service<user-login>` that provides a generated
``usersecret`` if there is none set up yet.

You should keep in mind that the recording survey, website and extra recording
fields might need to be set up in the iRecord's warehouse,
read more about that in :ref:`setting up a survey <survey-register>`.

Please check the :ref:`recording examples <send-record-example>`.

.. note:: To module will only check your app authorisation and warehouse information
  after which your request is proceeded to the Indicia's warehouse where the recording
  data is checked.

.. _user-login:

User authentication
-------------------

As with registering a new user account, signing in through the module
is through the same service endpoint ``'user/mobile/register'``.

Here the drupal user account details need to be provided:

- email
- password

On successful login, a new generated password is send back which could be used
to authenticate your records in the future.

The new password can be changed through iRecord interface by visiting
user account settings ``brc.ac.uk/irecord/user -> Edit -> Indicia mobile auth``
updating ``User shared secret`` field.

Please check the :ref:`example <user-login-example>`.

.. _user-register:

Registering with the website
----------------------------

To register with the website that the module is hosted at, an endpoint of
``'user/mobile/register'`` is used.

.. todo:: Add more information about the user registratin process.

Please check the :ref:`example <user-register-example>`.

.. _reports:

Accessing warehouse reports
---------------------------

The module allows to retrieve data from associated warehouse using its reports.
The endpoint for this is  ``'mobile/report'``.

Please check the :ref:`example <reports-example>`.
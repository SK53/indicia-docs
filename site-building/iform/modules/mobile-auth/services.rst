.. _services:

Services
========

The Mobile Authentication module provides the following  services:

- :ref:`user-register`
- :ref:`user-validate`
- :ref:`user-login`
- :ref:`send-record`
- :ref:`reports`

All the services the Mobile Auth module provides are accessed through a few
dedicated URLs using POST requests.

Before you can use these services a valid App secret and App name have to be set up.
Read more about :ref:`account-management`.

.. _user-register:

User registration
-----------------

To register a new user with the website that hosts the module, an endpoint of
``'user/mobile/register'`` is used.

The app must post the following inputs:

==========  =====================================================================================
Name        Value
==========  =====================================================================================
firstname   Required. A first name.
secondname  Required. A last name.
email       Required. An email address for the new user.
password    Required. A password for the new user account.
appname     Required (unless anonymous). Must match the app name that was configured.
appsecret   Required. Must match the app secret set for the app name in the module configuration.
==========  =====================================================================================

The following responses may be returned:

======  ======================  ======================================  ========================================
Status  Message                 Logged message                          Cause
======  ======================  ======================================  ========================================
400     Bad request             Missing parameter                       Email, password or appsecret missing.
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Invalid password        Password not strong enough              Zero length password.
400     Missing name parameter  First or secondname empty               Firsname or secondname empty.
200     *user secret*           Nothing                                 Successful registration of the user
                                                                        on the website returns the variables
                                                                        as indicated.
        *firstname*
        
        *secondname*
        
        *error*                                                         Possible error on registering with
                                                                        warehouse.
======  ======================  ======================================  ========================================

Please check the :ref:`example <user-register-example>`.

.. _user-validate:

Validation of new users
-----------------------

To register with the website that the module is hosted at, an endpoint of
``'user/mobile/activate/%/%'`` is used.

.. todo:: Add more information about the user registratin process.

Please check the :ref:`example <user-register-example>`.

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

.. _reports:

Accessing warehouse reports
---------------------------

The module allows to retrieve data from associated warehouse using its reports.
The endpoint for this is  ``'mobile/report'``.

.. todo:: Add more information about the access of warehouse reports.


Please check the :ref:`example <reports-example>`.

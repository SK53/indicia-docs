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
Status  Message                 Logged message (if enabled)             Cause
======  ======================  ======================================  ========================================
400     Bad request             Missing parameter                       Email, password or appsecret missing.
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Invalid email           Invalid email                           Fails the Drupal valid_email_address()
                                                                        test.
400     Invalid password        Password not strong enough              Zero length password.
401     Invalid password        Invalid password                        An email for an existing user has been
                                                                        supplied.
409     First or second name    First or second name missmatch          An email and password for an existing 
        missmatch                                                       user have been supplied.
400     Missing name parameter  First or secondname empty               Firsname or secondname empty.
200     | *user secret*         User *email* registered                 Successful registration of the user
        | *firstname*                                                   on the website returns the variables
        | *secondname*                                                  as indicated. This may end with any 
        | *error*                                                       error from user registration on the 
                                                                        warehouse.
======  ======================  ======================================  ========================================

The app needs to save the user secret that is returned on successful registration to use when submitting records.

Please check the :ref:`example <user-register-example>`.

.. _user-validate:

Validation of new users
-----------------------

Having sent a user registration request as described above, the user is sent an email to validate that the 
address is correct. Within the email is a link to click which calls the validation service.

The endpoint for validation is ``user/mobile/activate/%/%`` where the first % is substituted with the
Drupal user id and the second with a unique confirmation code. This is a simple GET request and there are 
no values to POST.

If the user id and confirmation code match with expected values then

#. The user account is enabled.
#. The user is redirected to a page of the website declared in the configuration.
#. If logging is enabled a message ``Activating user $uid with code $code`` is saved.

If the user id and confirmation code do not match with expected values then the user is simply redirected
to a page declared in the configuration. If the page to which the user is redirected is the <front> page, 
which is the default, the user will not be aware that there has been a problem.

User login
----------

A user may need to connect an app to an existing account on the host website under various circumstances.

* An app may allow a user to log out so that a different user may log in.
* A user may install the app on multiple devices.
* A user may have previously created an account via the host website.
* A host website may support multiple apps, one of which has previously created an account.

Logging in through the module uses the same endpoint as registering a new user account ``user/mobile/register``.

The app must post the following inputs:

==========  =====================================================================================
Name        Value
==========  =====================================================================================
email       Required. The email address for the existing user.
password    Required. The password for the existing user account.
appname     Required (unless anonymous). Must match the app name that was configured.
appsecret   Required. Must match the app secret set for the app name in the module configuration.
==========  =====================================================================================

The following responses may be returned:

======  ======================  ======================================  ========================================
Status  Message                 Logged message (if enabled)             Cause
======  ======================  ======================================  ========================================
400     Bad request             Missing parameter                       Email, password or appsecret missing.
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Invalid email           Invalid email                           Fails the Drupal valid_email_address()
                                                                        test.
400     Invalid password        Password not strong enough              Zero length password.
401     Invalid password        Invalid password                        The password was not correct.
400     Missing name parameter  First or secondname empty               The email was not that of an existing 
                                                                        user.
200     | *user secret*         | Creating new shared secret            Successful registration of the user
        | *firstname*           (if new shared secret needed)           on the website returns the variables
        | *secondname*          | Associating indicia user id           as indicated. This may end with any 
        | *error*               (if new id is needed)                   error from user registration on the 
                                | User *email* logged in                warehouse.
======  ======================  ======================================  ========================================

The app needs to save the user secret that is returned on successful log in to use when submitting records. It probably wants to save the firstname and secondname too, in order to report who is logged in.

Please check the :ref:`example <user-login-example>`.

.. _send-record:

Sending a record
----------------

When posting a record, the number of variables to be sent and the names of them depends upon how the survey has been configured in the warehouse. It also depends upon whether a sample is being sent with a single occurrence or with multiple occurrences. 

There is an option to send records without requiring user registration. This is highly discouraged as, though it lowers the initial barrier to recording, it results in an inferior user experience overall as a person's records can never be reliably accessed by them again.

The submission service endpoint is at ``mobile/submit``. 

The app must post the following basic inputs:

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
website_id              Required. The Indicia website_id of the Drupal site (23 for iRecord)
survey_id               Required. An Indicia survey_id belonging to the website_id in to which records will
                        be placed. The attributes that we post have to match those required by the survey.
                        (42 for iRecord General survey)
appname                 Required (unless anonymous). Must match the app name that was configured.
appsecret               Required. Must match the app secret set for the app name in the module configuration.
email                   Required for registered users. If not provided or not recognised then the record is 
                        submitted anonymously.
usersecret              Required for registered users and must match the value expected for the user. This is
                        returned by the registration/log in service.
======================  =====================================================================================

The sample inputs, some of which are required, are as follows:

==========================  =================================================================================
Name                        Value
==========================  =================================================================================
sample:date                 Required.
sample:entered_sref_system  Required. The system being used to submit the spatial reference. e.g.
                            OSGB for British National Grid
                            OSIE for Irish Grid
                            4326 for Latitude and Longitude in decimal form (WGS84 datum)
sample:entered_sref         Required. The spatial reference in the format defined by the above system e.g.
                            ``SJ70`` for a 10km OSGB grid square
                            ``SJ7404`` for a 1km OSGB grid square
                            ``SJ743047`` for a 100m OSGB grid square
                            ``SJ74350474`` for a 10m OSGB grid square
                            ``M98286465`` for a 10m OSIE grid square
                            ``51.43279N 2.57369E`` for a point using Lat/Long
sample:comment              Any plain text.
==========================  =================================================================================

The occurrence inputs for a single occurrence, some of which are required, are as follows:

=============================  ==============================================================================
Name                           Value
=============================  ==============================================================================
occurrence:taxa_taxon_list_id  Required. The id of the species name within a species list.
=============================  ==============================================================================

The survey-specific custom sample attributes, which have to conform with validation rules set on the 
warehouse, have the format ``smpAttr:*N* = *value*``

The sample attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
======================  =====================================================================================

The survey-specific custom occurrence attributes, which have to conform with validation rules set on the warehouse, have the format ``occAttr:*N* = *value*`` when submitting a single occurrence.

The occurrence attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
======================  =====================================================================================


The following responses may be returned:

======  ======================  ======================================  ========================================
Status  Message                 Logged message (if enabled)             Cause
======  ======================  ======================================  ========================================
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Bad request             User secret incorrect                   User secret missing or incorrect.
407     User not activated      User not activated                      The user is disabled in Drupal, probably
                                                                        because they have not followed the 
                                                                        activation link they were emailed after
                                                                        registration.
======  ======================  ======================================  ========================================
                                                                        


Record data:

- sample:date
- sample:entered_sref
- sample:entered_sref_system
- occurrence:taxa_taxon_list_id

*Authenticated record* submission adds a requirement: the record should go along with either
iRecord active *session cookie*, which would authenticate the user, or attaching to the record
user's ``usersecret`` along with its ``email``.

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

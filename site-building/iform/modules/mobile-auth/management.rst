.. _account-management:

Managing app accounts
=====================

Introduction
------------

The module allows the creation of multiple accounts for apps to authenticate with the host website using 
name-secret pairs. The accounts can be enabled/dissabled individually, as well as deleted and edited. It 
is expected that administrators will give app developers  permission to maintain their own accounts.

Create a new account
--------------------

To create an app account go to the configuration page by either 

* navigating to ``'admin/config/iform/mobile/dashboard'`` or
* selecting Configuration > IForm > Mobile Authentication in the admin menu.

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_dashboard_empty.png
    :alt: Mobile Auth module's dashboard

By clicking the link 'Add Mobile Application' at the bottom of the dashboard a blank
application account page is opened.

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_new_account.png
    :alt: Mobile Auth module's dashboard

Complete the form with the following information:

========================  ===================================================================================
Field                     Description
========================  ===================================================================================
Enabled                   This box must be checked to allow the app to communicate via this module.
Debug mode                If this box is checked, debugging information will be saved to the Drupal log.
                          Do not leave this enabled on a production site.
Title                     The title used to list the app in the configuration page.
App description           A description of the app that appears in the configuratin page.
App name                  This value must be included in any post to the services provided by this module.
App secret                This value must be included in any post to the services provided by this module.
========================  ===================================================================================

The following extra parameters may also be configured which relate to behaviour on user registration
through the app.

========================  ===================================================================================
Field                     Description
========================  ===================================================================================
Subject                   The subject line of the registration activation email. '!site' will be 
                          substituted with the website name.
Body                      The body of the activation email. '!activation_url' will be substituted with 
                          the link the user must follow to complete registration.
Redirection link          The url where users will be redirected to after clicking on the activation link.
Invalid redirection link  The url where users will be redirected to if following an expired or invalid
                          activation link.
========================  ===================================================================================

The anonymous app
-----------------

For backwards compatibility with  previous applications that all used a single
shared Appsecret without any Appname, there is an anonymous case introduced.

Saving an account with an App name of 'anonymous' allows you to authenticate your application using an
App secret only. New apps should not use this feature.

Multiple app secrets
--------------------

The module allows multiple application accounts to share the same App name; it allows the
creation of multiple App name-App secret pairs using the same App name.

This allows you to manage your applications in multiple ways. For example, in the case of multiple
mobile application versions there might be a need to disable one version (e.g. to dissable the
flow of records from old app versions) while keeping the other versions enabled.

Editing and deleting accounts
-----------------------------

Return to the configuration page to see a listing of your apps (or all apps if you have administrative permissions).
There are links in the table to edit and delete app settings.

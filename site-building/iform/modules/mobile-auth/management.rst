.. _account-management:

Managing app accounts
=====================

Introduction
------------

The module allows the creation of multiple accounts for apps to authenticate with the host website using name-secret pairs. The accounts can be enabled/dissabled individually, as well as deleted and edited.

Create a new account
--------------------

To create an app account go to the dashboard by either 

* visiting a link ``'admin/config/iform/mobile/dashboard'``
* selecting Configuration > IForm > Mobile Authentication in the admin menu or 
* visiting your personal dashboard (if the dashboard module is enabled and 'View personal dashboard' permission is granted). 

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_dashboard_empty.png
    :alt: Mobile Auth module's dashboard

By clicking the link 'Add Mobile Application' at the bottom of the dashboard a blank
application account page is opened.

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_new_account.png
    :alt: Mobile Auth module's dashboard


Anonymous case
--------------

For backwards compatibility with the previous applications that all used a single
shared Appsecret without any Appname, there is an anonymous case introduced.

Saving an account with an Appname of 'anonymous' allows you to authenticate your application using an
Appsecret only.

Multi Appsecrets
----------------

The module allows multiple application accounts to share the same Appname; it allows the
creation of multiple Appname-Appsecret pairs using the same Appname.

This allows you to manage your applications in multiple ways. For example, in the case of multiple
mobile application versions there might be a need to disable one version (e.g. to dissable the
flow of records from old app versions) while keeping the other versions enabled.

Options
-------

.. todo::
    Expand on account configuration options - debugging, emails etc.

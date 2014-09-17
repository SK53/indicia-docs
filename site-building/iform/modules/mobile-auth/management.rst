Managing app accounts
=====================


Intro
-----

The management of the mobile app authentication accounts is pretty straightforward.
The module allows to create multiple name-secret keys, which can be enabled/dissabled
individually, as well as deleted and edited.

Create a new account
--------------------

To create an app account you first need to have some minimum required permissions.
A site user with 'View personal dashboard' permission can access its personal dashboard,
where all the management lies.

The dashboard can be accessed by visiting a link *'admin/config/iform/mobile/dashboard'*
or through the admin menu (if shown to the user).

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_dashboard_empty.png
    :alt: Mobile Auth module's dashboard

By clicking the link 'Add Mobile Application' at the bottom of the dashboard a blank
application account page is opened.

  .. image:: ../../../../images/screenshots/drupal/modules/mobile_auth_new_account.png
    :alt: Mobile Auth module's dashboard


Anonymous case
--------------

To support backend compatibility with the previous applications that all used a single
shared Appsecret without any Appname, there is an anonymous case introduced.

Saving an account without an Appname allows you to authenticate your application using an
Appsecret only.

Multi Appsecrets
----------------

Module allows to share the same Appname with multiple application accounts; it allows the
creation of multiple Appname-Appsecret keys using the same Appname.

This allows to manage your applications in multiple ways. For example, in case of multiple
mobile application versions there might be a need to disable one version (etc. dissable the
flow of records from old app versions) while keeping the other versions enabled.

Options
-------

.. todo::
    Expand on account configuration options - debugging, emails etc.
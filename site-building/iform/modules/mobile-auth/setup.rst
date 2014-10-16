.. _setup:

Setting Up
==========

This section deals with setting up the module. The following information applies only
to website administrators. If you are an app developer and this module is being used to allow you to submit 
records through a website that you do not administer then you do not need to read this.

.. note:: This documentation covers only Drupal 7. The module is available for Drupal 6 but future development 
and support will target D7.

Prerequisites
-------------

The only requirement for setting up the Mobile Auth module is for the
**iForm module** to be installed and configured on your Drupal site.


Installation
------------

Currently (Oct 2014) you need to check out the module from our repository using Subversion:

``svn co http://indicia.googlecode.com/svn/drupal_7/modules/iform_mobile_auth/trunk/iform_mobile_auth``

This is the development version. There is no released version at present. Indeed some of the 
features described are still in a branch and have not yet been merged with the trunk.

Depending on your Drupal installation the module should be placed in your
modules folder -``sites\all\modules``.

Setting permissions
-------------------

The module provides two permissions:

* View the administrative dashboard
* View personal dashboard

A user must be assigned one of these permissions in order to manage app accounts.

The only difference is that a person with Administrator permissions can
access and modify all existing application accounts on the site, while the
user can only see and edit those of his creation.


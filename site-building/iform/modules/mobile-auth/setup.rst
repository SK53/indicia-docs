.. _setup:

Setting Up
==========

This section deals with setting up the module. The following information applies only
to website administrators. If you are an app developer and this module is being used to allow you to submit records through a website that you do not administer then you do not need to read this.

.. note:: This documentation covers only Drupal 7.

Prerequisites
-------------

The only requirement for setting up the Mobile Auth module is for the
**iForm module** to be installed and configured on your Drupal site.


Installation
------------

You can download the module from Indicia's :ref:`Downloads page<http://www.indicia.org.uk/downloads>`
or checking it out from our repository using Subversion:

``svn co https://indicia.googlecode.com/svn/drupal_7/modules/iform_mobile_auth/trunk/iform_mobile_auth``

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


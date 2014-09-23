.. _setup:

Setting Up
==========

This section deals with the setting up process of the module. Since all the functionality
is set up on iRecord website, the following information applies only
to those who want to install their own system of recording.

.. note:: This documentation covers only Drupal 7.

Prerequisites
-------------

The main and only requirement for setting up Mobile Auth module is the
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

There are two types of permissions that the module provides:

* Administrator
* User

The main and only difference is that a person with Administrator permissions can
access and modify with all existing application accounts on the site, while the
user can only see and edit those of his creation.


######################
Upgrading Drupal Files
######################

For ALL upgrades, it is advisable to first test the upgrade on a development version of
your website and also to have a backup of the Drupal files and database before performing
the upgrade, in case something untoward happens. 

Upgrading Drupal core
=====================

One skill you'll want to pick up at some point is how to keep everything up to date. 
Keeping your site up to date helps to ensure that you have the most efficient, secure and
reliable version available. There are plenty of existing resources on how you should 
correctly upgrade your Drupal installation, which as long as you are doing a minor version
upgrade (as opposed to a major version, e.g. from Drupal 6 to 7) is generally quite 
simple. See `upgrading Drupal core <https://drupal.org/taxonomy/term/34882>`_ for the 
official documentation. 

Upgrading Drupal modules
========================

For modules downloaded from Drupal.org, you can upgrade them by copying the files over
then visiting the ``update.php`` path on your website. Review the **Available updates**
report occasionally to look for modules which need to be upgraded. Read the `official 
documentation on how to upgrade modules <https://drupal.org/node/250790>`_.

Upgrading Indicia modules
=========================

Because Indicia themes and modules are very specific and not really of interest to the 
rest of the Drupal community, they are kept along with the other Indicia code on the
`Downloads page <http://www.indicia.org.uk/downloads>`_ site rather than on `drupal.org 
<http://drupal.org>`_. Therefore the update process is different. 

You may also, on occasion, want to download a particular version directly from Github (the 
place used to hold all Indicia code). This allows you to access any copy of a module
or theme including the latest development. If you visit `Indicia Team on Github 
<https://github.com/Indicia-Team>`_ and select the repository of interest there is a 
"Clone or download" button which, by default, gets the latest release from the master
branch. You can switch to the develop branch to get the latest development version.

There are several modules available for Indicia to integrate with both Drupal 6, 7 & 8. In
all cases you need to download and unzip the module folder(s), then copy the
folder(s) to your ``sites/all/modules`` folder on your webserver, using an FTP client or
other file access if required to access the remote server. Although most updates will not
require it, you should visit Drupal's ``update.php`` path after installation in case there
are any database schema updates required.


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

Upgrading Indicia code
======================

Because Indicia themes and modules are very specific and not really of interest to the 
rest of the Drupal community, they are kept along with the other Indicia code on the
`Downloads page <http://www.indicia.org.uk/downloads>`_ site rather than on `drupal.org 
<http://drupal.org>`_. Therefore the update process is different. Formal releases of code
were originally all available from the `Google Code Downloads page 
<http://code.google.com/p/indicia/downloads/list>`_, though this facility is in the 
process of being withdrawn by Google, so new downloadable releases will be made available
from `indicia.org <http://www.indicia.org.uk/downloads>`_. 

You may also on occasion want to download a release directly from Subversion (the 
repository used to hold all Indicia code). This allows you to access the very latest copy
of a module or theme. If you want to do this you will need to ensure that you have a
Subversion client installed on your machine. This is often provided on Linux & Mac OS X
installations (type ``svn help`` in a terminal window to check this). On Windows you might
like to install `TortoiseSVN <http://tortoisesvn.net/>`_ which integrates Subversion 
functionality into the context menu of Windows Explorer, or `slick subversion 
<http://www.sliksvn.com/en/download>`_ if you prefer the command line approach. If you are
simply trying to get the latest code in order to copy to your webserver, then in all 
cases you will need to create a local folder in which to obtain the code. Navigate to that
folder using the appropriate tool (e.g. Windows command prompt for slik subversion, 
Windows Explorer for TortoiseSVN, or a terminal window for Linux/Mac OS X). Then issue
an SVN Export command specifying the path to the resource you want to obtain, for example
this command gets the latest **iform** module for Drupal 7::

  svn export http://indicia.googlecode.com/svn/drupal_7/modules/iform/trunk/iform
  
If you are using TortoiseSVN, then there is a TortoiseSVN menu item on the context menu
if you right click on the folder. 

Upgrading Indicia modules
=========================

There are several modules available for Indicia to integrate with both Drupal 6 & 7. In
all cases you need to download and unzip or export the module folder(s), then copy the
folder(s) to your ``sites/all/modules`` folder on your webserver, using an FTP client or
other file access if required to access the remote server. Although most updates will not
require it, you should visit Drupal's ``update.php`` path after installation in case there
are any database schema updates required.

The following SVN commands are available.

#. Extract the latest version of the iform module code for Drupal 7, which is the primary 
   module used to integrate Indicia into Drupal::

     svn export http://indicia.googlecode.com/svn/drupal_7/modules/iform/trunk/iform
     
#. Extract the latest version of the indicia features modules for Drupal 7, which provide
   several installable features to setup common site patterns such as recording groups
   and Explore reports::
   
     svn export http://indicia.googlecode.com/svn/drupal_7/modules/indicia_features/trunk/indicia_features

#. Extract the latest version of the iform module code for Drupal 6::

     svn export http://indicia.googlecode.com/svn/drupal/modules/iform/trunk/iform
     
#. Extract a previous release of the iform module code for Drupal 6::

     svn export http://indicia.googlecode.com/svn/drupal/modules/iform/branches/version 0.8.1/iform
     
   See `Google Code <http://code.google.com/p/indicia/source/browse/#svn%2Fdrupal%2Fmodules%2Fiform%2Fbranches>`_
   to check the available versions.

#. Extract the latest version of the indicia features modules for Drupal 6, which provide
   several installable features used to create Instant Indicia setups::
   
     svn export http://indicia.googlecode.com/svn/drupal/modules/indicia_features/trunk/indicia_features

Upgrading Indicia themes
========================


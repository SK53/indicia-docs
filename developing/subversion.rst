**********
Subversion
**********

Why use version control?
========================

Indicia's code is hosted on the `Google Code <http://code.google.com/p/indicia/>`_ 
website. This website provides facilities for hosting downloadable release 
versions of the code as well as a repository containing every code file being
worked on. The repository, called a version control system, maintains:

* a master copy of every single source file.
* an audit trail of every single change to any source file, including notes, 
  date and authorship of every change.

There are several popular version control systems in use for open source 
projects; Indicia uses one called `Subversion <http://subversion.apache.org/>`_ 
because it is fairly simple to understand and use as well as being well 
supported by many development tools. When using a version control system,
rather than edit the files directly on the shared repository, developers make
a local copy of all the code files and work on them there. When happy that the
change they are implementing is ready, they push the changes back up to the 
server copy and other developers then merge those changes back into their copies
of the code. Subversion includes tools for viewing the differences between files,
resolving any conflicts that may occur and rolling back any changes subsequently
deemed to be unwanted. Subversion also allows you to *tag* versions of the code
at a point in time (tags are normally used to store a copy of the released
versions of the code) and to *branch* the code giving a parallel set of code to 
work on. Branches can be useful for several reasons, one of which is to create
an environment in which you can safely experiment with the code without 
affecting the master copy until you are satisfied that the experiment has 
succeeded. If it fails, just delete the branch!

Without a source control such as Subversion, working as a collaborative team 
would be a quagmire of accidental overwrites of each other's changes, 
untraceable mistakes and other such nightmares.

.. note::

  If you are not familiar with Subversion or version control in general then 
  there are several primers available on the web, for example the 
  `Subversion manual <http://svnbook.red-bean.com/>`_ contains chapters on 
  Version Control Basics and Version Control the Subversion Way which provide a 
  good starting point.

Obtaining Indicia's code
========================

Indicia's code can be obtained in either of the following ways:

* By downloading releases from the `Downloads <http://code.google.com/p/indicia/downloads/list>`_ 
  tab of the Google Code site.
* By using the Subversion source control system to obtain the latest or any 
  other code version at any point in time.

As we are interested in learning to develop Indicia code, we'll focus on the 
latter. Although it is possible to browse the code via the 
`Source tab's Browse subsection <http://code.google.com/p/indicia/source/browse/>`_
on the Google Code site, in most cases you will want to use a *Subversion 
client* to access the code. A subversion client is simply a piece of software
installed on your local machine that can interact with the Subversion server
where the code is held. There are many options available and the best one will 
depend on your choice of development operating system and code editor. For 
Windows use a popular choice is `TortoiseSVN <http://tortoisesvn.net/>`_ but
you may also find that the development tool you are using already has built in
integration with Subversion. 

Trunks, branches and tags
=========================

Subversion keeps code in a tree structure which maps to a folder structure on 
your disk. By convention it splits the code for each project or sub-project into 
3 folders:

* *trunk* - This folder contains the latest 'bleeding edge' code and is the one 
  that developers actively commit changes into when they become part of the 
  project core. Although it is not good practice to knowingly commit changes 
  into the trunk which will break the project, it is also not expected that 
  every change will be fully tested for production when it is committed. 
  Therefore the trunk code should not be used for production servers.
* *branches* - A branch is a copy of the code which is being maintained 
  alongside the trunk for one reason or another. For example, a branch might be 
  created when a developer wants to develop a feature and not commit the feature 
  to the trunk until the feature is ready. Or a branch could be created for a 
  developer to write experimental code against. The advantage of using a branch 
  in Subversion over just creating a copy of the code on your disk is that you 
  get full change tracking and other useful features of SVN within the confines 
  of your branch.
* *tags* - A tag is a snapshot of the code taken at a point in time. In Indicia 
  we use tags to keep copies of the released code that was used for stable 
  downloads for future reference.

Terminology
===========

There are a few variations on terminology used alongside version control systems
but for Subversion the following terms apply:

* **checkout** - obtaining a local copy of the code held in Subversion
* **update** - updating a local copy of code that was previously checked out
  from Subversion
* **commit** - uploading local changes into the Subversion source repository
* **merge** - updating a local copy of code which has changed both locally
  and on the Subversion repository
* **conflict** - the result of a **merge** when one section of the code has 
  changed both locally and on the repository so that automatic merging cannot
  take place. Subversion clients tend to provide tools for **conflict 
  resolution**
* **diff** - a view of the differences between 2 versions of the same file, 
  e.g. the local copy and the master copy.

Navigating the Indicia repository
=================================

Warehouse
---------

The warehouse code is found at http://indicia.googlecode.com/svn/core/trunk/
(use http for read-only access or https for read-write access if you have commit 
rights to the project).

When there is a version of the Indicia warehouse which is in testing and nearly 
ready for release it will be found under http://indicia.googlecode.com/svn/core/branches/
in a folder named after the version. This allows developers to continue 
developing against the trunk without risking adversely affecting the release. At
this stage, when a developer finds an important bug in the trunk which also 
exists in the version branch, they should commit that bug to the branch as well 
as long as they consider that there is no risk of knock-on effects on the rest 
of the code. Likewise any bugs found during the testing of the version branch 
must be fixed in both the branch and the trunk code.

Any formally released versions of the warehouse are kept under
http://indicia.googlecode.com/svn/core/tags/.

To summarise if you want to obtain a stable version of the warehouse, you can 
obtain it from the downloads page or via the tags folder in Subversion. For a 
pre-release of the next version visit the branches folder (if one is available 
at that point in time). For the latest bleeding edge code use the Subversion 
trunk folder

IForm Module
------------

The second sub-project within Indicia's source code is the Drupal IForm 
integration module. The source code for this is held under
http://indicia.googlecode.com/svn/drupal/modules/iform, with branches, tags
and trunk sub-folders as before. Within the iform code we use *svn:external*,
which is a definition that the iform code should include some code held 
elsewhere when you obtain a copy of the code. This allows the IForm module to 
include a copy of the *media* and *client_helpers* folders from the warehouse's
code so there is no need to maintain 2 physical copies of the code which is 
being used in 2 different contexts.
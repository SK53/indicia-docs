**************************
GitHub and version control
**************************

Why use version control?
========================

Indicia's code is hosted on `GitHub <https://github.com/Indicia-Team/>`_. For a quick
primer, read this article explaining what GitHub is on `How-to-Geek 
<http://www.howtogeek.com/180167/htg-explains-what-is-github-and-what-do-geeks-use-it-for/>`_.

This website provides a repository containing every code file being worked on. 

There are several popular version control systems in use for open source projects; Indicia
uses one called `Git <https://git-scm.com/>`_ because it is now the most widely used in
the open source community. When using a version control system, rather than edit the files
directly on the shared repository, developers make a local copy of all the code files and
work on them there. When happy that the change they are implementing is ready, they push
the changes back up to the server copy and other developers then merge those changes back
into their copies of the code. Git includes tools for viewing the differences between
files, resolving any conflicts that may occur and rolling back any changes subsequently
deemed to be unwanted. Git also allows you to *tag* versions of the code at a point in
time (tags are normally used to store a copy of the released versions of the code) and to
*branch* the code giving a parallel set of code to work on. Branches can be useful for
several reasons, one of which is to create an environment in which you can safely
experiment with the code without affecting the master copy until you are satisfied that
the experiment has succeeded. If it fails, just delete the branch! Branches are also used
to keep the current stable version of the code separate from the 'bleeding edge' code that
developers are currently working on.

Without a source control system such as Git, working as a collaborative team 
would be a quagmire of accidental overwrites of each other's changes, 
untraceable mistakes and other such nightmares.

Key Points
==========

  * Indicia’s code is hosted on GitHub, under the Indicia-Team organisation, 
    https://github.com/Indicia-Team.
  * The project is divided into repositories for the warehouse, client libraries, plus 
    Drupal version specific themes and modules. For example the Drupal 7 Indicia forms 
    module repository is at https://github.com/Indicia-Team/drupal-7-module-iform. 
  * Our Git workflow is based on the model proposed at 
    http://nvie.com/posts/a-successful-git-branching-model.
  * All repositories have a history of changes to the code, and the current state of the 
    code exists in several “branches” - at least a master and a develop branch. The master 
    branch should always reflect the stable production ready code. The develop branch 
    contains development changes to the code which may not be production ready. Other 
    branches may exist either as a result of the migration from Google code or for current
    development needs.
    
Glossary
========

For a full glossary of Git terms, see https://help.github.com/articles/github-glossary. 
The list below covers some of the key ones we'll be using for Indicia code management.

  * Branch - a parallel version of the code in a repository, for example there can be a
    stable branch, a branch for the bleeding edge development code, plus branches for 
    specific features under development.
  * Clone - copy a repository to a different location, for example to copy the warehouse
    code from GitHub to a local development environment. Because Git is a distributed 
    version control system as opposed to a centralised one, each clone is a full copy
    of the repository and you can commit changes to it, work on it offline etc. Clones
    remain synced with the repository they were copied from and can be easily synced.
  * Checkout - 
  * Commit - an individual change to a file or a set of files which create a new revision
    of those files. 
  * Fork - to copy a repository to a different GitHub account. The fork can then be worked
    on independently or a pull request issues later to ask for changes to be merged back
    in.
  * Merge - to take the changes from one branch and merge them into another.
  * Origin - an alias for the URL of the repository on GitHub which contains the accepted
    master copy of the code. 
  * Pull - fetching changes to a file from the remote version of that file into your 
    local copy and merging them.
  * Pull request - a proposal that changes submitted to a repository are to be accepted
    into the repository. In Git, a developer without commit rights can fork a repository
    and work on their own, then issue a pull request to ask for their changes to be
    accepted.
  * Push - to send locally committed changes from a local repository to a remote 
    repository.
  * Tag - to mark a point in the history of a repository as significant, for example to 
    mark the point at which a release was made. 

I'm not an Indicia contributor and I want to ...
================================================

...get the latest stable code from a repository
-----------------------------------------------

  #. Follow the link for the repository you need the code for from the main `Indicia-Team 
     github page <https://github.com/Indicia-Team/>`_.
  #. Use the **Download ZIP** button on the right of the page.

...get the latest development code from a repository
----------------------------------------------------

  #. Follow the link for the repository you need the code for from the main `Indicia-Team 
     github page <https://github.com/Indicia-Team/>`_.
  #. Click on the **Branch: master** drop down button and select **develop** from the menu
     that appears.
  #. Use the **Download ZIP** button on the right of the page.

...clone a repository to your local machine
-------------------------------------------

Using your command line client, navigate to the folder you want the code copied to. In 
this case, the modules folder of our Drupal install.:: 

  cd sites/all/modules

Clone the repository to your local machine, remembering to specify the folder name you 
want the repository to clone into. You can get the Clone URL from the repository home page
on GitHub (https://github.com/Indicia-Team/drupal-7-module-iform_mobile_auth).::

  git clone https://github.com/Indicia-Team/drupal-7-module-iform_mobile_auth.git iform_mobile_auth

That’s got you a copy of the code. You’ll be pointing to the default branch (master – the 
stable code). You can check this by typing::

  git branch

That’s shown you just the branches you’ve got locally – only one so far. Type the 
following to check the available remote branches::

  git branch –r
  
If you want to switch to the bleeding edge develop version of the code::

  git fetch
  git checkout develop
  
Now, just toggle between master or develop by typing::

  git branch master

Or::

  git branch develop

Propose a change to the code
----------------------------

.. todo::

  Document how to create a pull request as a non-contributor.

I am an Indicia contributor and I want to...
============================================

...hotfix some live code 
------------------------

Sometimes it is necessary to release a change to the live master version of the code in a
repository without waiting for the next time the develop code branch is released to live.
This is called a hotfix since it bypasses the normal develop branch then release cycle.
Here are the steps required:

Create a branch called hotfix-* off of the master branch of the relevant repository::

  git checkout -b hotfix-myfix master
  
Make your required code changes in this branch, test and commit them.

If your repository has a version number file (e.g. `application/config/version.php` then
bump the version number and commit it. 

.. todo::

  What happens if the application version and database version are then out of step on the
  warehouse?

Publish/push your hotfix branch to the GitHub repo::

  git push origin hotfix-myfix

Login to GitHub and find the repository you are working on. Switch to your hotfix branch
then click the Pull request button. Make sure that the base is set to master and follow
the steps to create the pull request, check the changes then merge it.

Repeat the last step to merge the hotfix into the develop branch as well.

In GitHub, add a release to tag the new version number against the code.

.. tip::

  Merging into the develop branch might not work without many conflicts, due to the legacy
  of migration from Google Code. This issue should disappear once we start doing full 
  releases from the GitHub code. If that is the case, then you can simply repeat the 
  bugfix commit and version bump into the develop branch.

...develop a new feature
------------------------

...make a release
-----------------

    
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
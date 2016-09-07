.. _documentation-tutorial:

**********************************************
Contributing to the Documentation - a Tutorial
**********************************************

Let's run through the steps needed for you to start contributing to the documentation. It is worth noting that this tutorial has been written on a Mac using Mac OS X (10.7 Lion), some of the steps you perform may vary if your computer configuration is different, however the basic principles will still be the same.

You should have read the overview, :ref:`documentation`, first. To reiterate, We hold a repository of all the ReStructureed Text (RST) documents we are working on in Git. The administrator of the documentation website then converts the RST into HTML for use on the public website. We'll install a **Git client** to allow us to add our RST format documentation to the controlled central repository. We'll use **Sphinx** to create a preview of what the final HTML of any documentation we create will look like as all the documentation we upload to Git is in RST format.

Getting to Grips with Git
=========================

Let's start by taking a look at Git. Git is a source control system used for organising and controlling files. It gives us a way of controlling and organising the documentation we are writing. For instance, we need to avoid people overwriting other contributors' work by accident and it is also useful to track who has changed a particular document. In reality this is just a small selection of the kinds of control that need to be applied during the development of our documentation.

The documentation is hosted on a website called **github** so our first task to is to register and get a login for that website.

https://github.com/

Once registered, you will you need to post a request to join in the documentation on the `forum <http://forums.nbn.org.uk/viewforum.php?id=25>`_ so you can be added to the project team. When working with documentation you won't be logging onto the website directly, you will use a **Git Client**. Before downloading a Git client, let’s have a quick look at how GIT works.

The central RST documentation repository is held on the Internet on the github website. When you install a Git client you are actually taking a **copy** of the whole file repository for the project on your computer. You can then make changes to the documentation in the local repository and when you are happy with the changes, you can **commit** the changes to the local repository. Once committed we can **push** these changes to the main repository on github.

.. image:: images/git_workflow.*

**Push** – Any changes you have made to your local repository are placed in the main repository held on the Internet.

**Pull** – If anyone else has made changes to the main repository, then these are moved onto your local repository.

**Commit** – When you complete a change, you “commit” it to the local repository. By doing this we ensure the local repository doesn’t become full of half-finished work. At a convenient point when all your changes are finished you can **push** them to the internet.

In reality these actions can be broken down into even smaller actions such as **fetch** and **merge**. It is beyond the scope of these document to cover all the actions that can be performed with Git, however there is plenty of information available about Git on the Internet when you are ready to further your understanding.

There are many GIT client applications available, so feel free choose your own one to use.
We will take a look at the client called `GitHub <http://mac.github.com/>`_. This client only works in Mac Os X Lion (10.7) or above, but the principles of this tutorial apply to other clients as well. `Source Tree <https://www.atlassian.com/software/sourcetree>`_ is a suitable client for Windows.

.. tip:: Don't get confused between the github website and the GitHub client software even though they have the same name.

Once downloaded, double-click on the GitHub application, it will ask you to enter your login name and password for the github website. Once you have entered this information, GitHub will open. You need to then check the settings in your Git client to make sure they are correct.  Make sure your Primary Remote Repository (under the Settings tab in GitHub) is pointing at the following URL, if it is different then you need to change it (some GIT clients may not fill it in at all for you)

https://github.com/Indicia-Team/indicia-docs.git

At the top of the GitHub window click on **Repositories** *(next to the green, yellow, red button window controls)*. Go to **My Repositories** in the side menu and right-click *(or ctrl-click on a one-button mouse)* on any existing repositories and select to remove the item. You might have already been linked to the correct repository, but for the purposes of this document it ensures we are all starting from the same point.
In the side menu, click on **Indicia-Team** (If you cannot see this, it means the request you made on the `forum <http://forums.nbn.org.uk/viewforum.php?id=25>`_ to join the documentation team has not been accepted yet). Click on the **Clone to Computer** button. Select a suitable place to save the file. This makes a copy of the documentation and holds it on your computer, you can then edit the documentation on your computer before uploading it when you are happy with it.
Click on My Repositories and you will see the single repository you downloaded. Double-click on the repository and then click on the Changes tab. You will see a Commit button.

.. image:: images/changes_tab.*

Let's make some changes to the documentation. In the GitHub client, double-click on the indicia-docs folder underneath the "Select All" checkbox. This will open a window allowing you to browse for files associated with the documentation repository.

.. image:: images/documentation_tree.*

We are going to edit a file, we only need to make a very small change *(such as changing a single character)*. Do not change any text which has been marked as "todo" as this text is automatically omitted from view on the central repository.
Have a look on the documentation site for a suitable page to edit and find the equivalent .rst file in the documentation files tree window that opened on your local machine *(see image above)*. Open the file in a plain text editor, make your small change and save and close the file.

Return to the GitHub "Changes" tab. You will see a preview of the change you made. You are now going to "Commit" the change. Don't forget the change doesn't appear in the main repository even after the **Commit** as we have not pushed it to the Internet yet.

In the **Commit summary** box, type in "Small change to test GitHub". In the **Extended description**, write a description of what you have changed. Also mention that it is just a test so the administrator knows not to include the change when the HTML is built.
When you have done this, click on the Commit button.

Our next task is to click on the **Sync** button, when you do this you may be asked to enter your username and password. The Sync button pulls any changes from the main repository into your local repository and pushes the change you make back to the main repository. This is a specific feature of the GitHub client, other client's might not have a Sync button at all and instead might only implement push and pull separately.

Once we have done this, our change will have been uploaded to the main repository held on the Internet. Navigate to the `repository <https://github.com/indicia-team/indicia-docs/>`_ in your web-browser. A page will be displayed showing the contents of the repository in a tree structure.

.. image:: images/repository.*

Locate the file you edited in the tree, notice that the structure of the tree of files actually mirrors the documentation tree on your computer so the document will be easy to find. Open the file to see your change.
Remember that once you have pushed the documentation change to the internet, it doesn’t appear on the Indicia documentation website until the project documentation leader builds the HTML *(in a similar way you build HTML using Sphinx on your local machine)*.

.. tip:: RST needs to be written in a plain text file (not .rtf or any other format). When you save the file with the .rst extension make sure the computer doesn’t add an extra .txt extension on the end automatically. This may be hidden from view and will stop Sphinx from processing the file *(On the Mac you can see a hidden extension by click on the file and going to the File menu and selecting “Get Info”)*.

Creating HTML with Sphinx
=========================

The documentation we write in RST is converted to HTML with Sphinx. To install Sphinx, refer to :ref:`documentation-mac` or :ref:`documentation-windows`

Let’s create some content for Sphinx to process. Create a file called page1.rst with the following RST inside it. ::


   my header
   =========
   Plain text, *italic text*, **bold text**.

This file needs to be placed in the root folder of the documentation. We aren’t quite ready to process the file yet though, we still need to edit the contents.rst file that can be found in the same folder.

.. note::

   The contents.rst is a special file holding the top-level table of contents (..toctree:: in Sphinx-speak). In general, every folder has an index.rst file which contains a table of contents for that section.

When you initially open the file it will look something like this,

.. image:: images/initial_index.*

We just need to add an extra line so it looks like this,

.. image:: images/index_altered.*

Pay attention to make sure you enter the indentation and the blank lines correctly.

Go to the command line and navigate to the root folder  and run the following command ::

   sphinx-build . _build

.. tip:: If you have "make" installed on your computer, this command can be replaced with "make html". If you have configured PHP Storm with file watchers (see :ref:`documentation-windows`) to run the build then it will have happened automatically on saving the file.

This will create the HTML files for the documentation inside a folder called **_build/html** which can be found inside the root folder. Once processing is completed, double-click the contents.html file in this folder. A HTML page will open in your default browser, in the Contents section of the page there will be a link called “my header” which will link to your new page.

Overview
========

On completion of this tutorial you should:

* Have an appreciation of how RST documents are structured.

* Understand how to install the RST document convertor **Sphinx** and what it is used for.

* Have a good understanding of what **github** does and understand the document workflow from raw RST on your home computer to HTML on a live public-facing website.

* How to install and use the GitHub Git client software.



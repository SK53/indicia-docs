Contributing to the documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's run through the steps needed for you to start contributing to the documentation.
We'll install the software components you'll need and also take a look at how to use them.
Before we start it is worth noting that this tutorial has been written on a Mac using Mac
OS X (10.7 Lion), some of the steps you perform may vary if your computer configuration is
different, however the basic principles will still be the same.

Before jumping straight into explanations of how to install the software components we
need, let's take a quick look at what these systems actually do.

A good starting point is to take a look at `restructuredText (RST, reST)
<http://sphinx.pocoo.org/rest.html>`_ as this is the text format we'll be writing our
documentation in.

RST is fast, simple and powerful. If you look at a RST document, you'll see that the
formatting information is contained as part of the text itself, so the text does not
actually look like the final output. The document is then processed to change it into the
final HTML page. Here is a quick example of what some simple RST text might look like.

.. image:: images/rst_example.*

The first piece of software we will install in this tutorial is called **Sphinx**, it
allows us to convert RST documents into HTML.

We will also learn about the **Git** source control system, this gives us a way of
controlling and organising the documentation we are writing. For instance, we need to
avoid people overwriting other contributors' work by accident and it is also useful to
track who has changed a particular document. In reality this is just a small selection of
the kinds of control that need to be applied during the development of our documentation.

In Git we hold a repository of all the RST documents we are working on, the administrator
of the documentation website then converts the RST into HTML for use on the public
website. We'll install a **Git client** to allow us to add our RST format documentation to
the controlled central repository. We'll use **Sphinx** to preview what the final HTML of
any documentation we create will look like as all the documentation we upload to Git is in
RST format.

To install Sphinx you'll need to be connected to the Internet. The installer uses `Easy
Install <http://packages.python.org/distribute/easy_install.html>`_ which is built-in to
Mac OS X. Firstly you'll need to open the system command line by navigating to your
computer's Applications folder, opening the Utilities folder before double-clicking on the
Terminal application. Type in the following command and press return. ::

  sudo easy_install sphinx

The system will then automatically download and install Sphinx. Let's run through the
setup process for a Sphinx project. Type the following command and press return. :: 

  sphinx-quickstart

At this point the system will ask you a series of questions on how to setup Sphinx. There
are quite a lot of questions, so here is a quick guide. You will only be using Sphinx to
preview the HTML output so do not worry if your answers differ slightly from the answers
given here as they are only intended to be a guide.

* Q: Root path for the documentation
	A: **/Sphinx/Documentation/**
	*(This is only a suggestion so feel free to choose your own path)*

* Q: Separate source and build directories?
	A: **y**

* Q: Name prefix for templates and static dir
	A: **_**
	*(underscore)*

* Q: Project Name
	A: **Indicia**

* Q: Author name(s)
	A: *Enter your full name*

* Q: Project version
	A: **1**

* Q: Project release
	A: **1**

* Q: Source file suffix
	A: **.rst**

* Q: Name of your master document
	A: **index**

* Q: Do you want to use the epub builder?
	A: **n**

* Q: autodoc: automatically insert docstrings from modules?
	A: **n**

* Q: doctest: automatically test code snippets in doctest blocks?
	A: **n**

* Q: intersphinx: link between Sphinx documentation of different projects?
	A: **n**

* Q: todo: write "todo" entries that can be shown or hidden on build?
	A: **n**

* Q: coverage: checks for documentation coverage?
	A: **n**

* Q: pngmath: include math, rendered as PNG images?
	A: **n**

* Q: mathjax: include math, rendered in the browser by MathJax?
	A: **n**


* Q: ifconfig: conditional inclusion of content based on config values?

	A: **n**

* Q: viewcode: include links to the source code of documented Python objects?
	A: **n**

* Q: Create Makefile?
	A: **y**

* Q: Create Windows command file?
	A: **y**

*Phew all done!!*

You can now go to the folder you specified in the first question and you will see it is populated with various items such as **build** and **source** folders.

.. image:: images/sphinx_folder.*

.. tip:: RST needs to be written in a plain text file (not .rtf or any other format). When you save the file with the .rst extension make sure the computer doesn’t add an extra .txt extension on the end automatically. This may be hidden from view and will stop Sphinx from processing the file *(On the Mac you can see a hidden extension by click on the file and going to the File menu and selecting “Get Info”)*.

Let’s create some content for Sphinx to process. Create a file called page1.rst with the following RST inside it.


.. image:: images/rst_example.*

This file needs to be placed in the **source** folder. We aren’t quite ready to process the file yet though, we still need to edit the index file that can be found in the same folder. 

When you initially open the file it will look like this,

.. image:: images/initial_index.*

We just need to add an extra line so it looks like this,

.. image:: images/index_altered.*

Pay attention to make sure you enter the indentation and also the blank lines either side of the new line correctly.

Go to the command line and navigate to the same folder as the index.rst file and run the following command *(changing the folder name if you gave your _build folder a different name)*

sphinx-build . _build 

.. tip:: If you have "make" installed on your computer, this command can be replace with "make html"

This will create the HTML files for the documentation inside a folder called **_build** which can be found inside the source folder. Once processing is completed, double-click the index.html file in the _build folder. A HTML page will open in your default browser, in the Contents section of the page there will be a link called “my header” which will link to your new page.

Now let's take a look at using Git. As I described earlier, Git is a source control system used for organising and controlling documentation.
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
We will take a look at the client called **GitHub**. This client only works in Mac Os X Lion (10.7) or above, but the principles of this tutorial apply to other clients as well.

.. tip:: Don't get confused between the github website and the GitHub client software even though they have the same name.

You can get the GitHub client software `here <http://mac.github.com/>`_.

Once downloaded, double-click on the GitHub application, it will ask you to enter your login name and password for the github website. Once you have entered this information, GitHub will open. You need to then check the settings in your Git client to make sure they are correct.  Make sure your Primary Remote Repository (under the Settings tab in GitHub) is pointing at the following URL, if it is different then you need to change it (some GIT clients may not fill it in at all for you)

https://github.com/Indicia-Team/indicia-docs.git

Your Git client takes copy of the main repository. When this copy is taken, it includes setup files the computer uses to maintain the repository’s structure. 
Git Clients usually include the ability to ignore such files so you cannot see them on screen and you can't accidentally edit and upload them. You can change the ignore file used to store these details. Once again this will vary slightly depending on your Git Client. In GitHub the ‘Ignore files’ can be accessed under the **Settings** tab. Change the ignore file to show the following (You need replace the “_build” with the name of the folder that Sphinx is setup to build to if you chose another folder name),

.. image:: images/ignore_file.*

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

*Exercise*

*See if you can now use Sphinx to generate a HTML preview of all of the documentation for the project. Remove your current local repository and do a Clone to Computer again to save it as a Sphinx source folder. Don't forget to take a backup of the current Source folder so you can revert to it if required.*


**Overview**

On completion of this tutorial you should be familiar with the following.

* Have an appreciation of how RST documents are structured.

* Understand how to install the RST document convertor **Sphinx** and what it is used for.

* Have a good understanding of what **github** does and understand the document workflow from raw RST on your home computer to HTML on a live public-facing website.

* How to install and use the GitHub Git client software.



.. _sphinx-setup:

*****************
Setting up Sphinx
*****************

If you are working on the documentation in the Indicia repository there is no need to do anything to set up Sphinx as the repository contains the necessary configuration files. However, if you are starting a new document repository for some reason then the following information may be useful.

At a commnand prompt, type the following command and press return. ::

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


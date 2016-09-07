.. _documentation-mac:

*****************************************************
Installing and Using the Documentation Tools on a Mac
*****************************************************

Clone the Documentation Repository
==================================

Fork and clone the documentation at https://github.com/Indicia-Team/indicia-docs. You can now add or edit files in your local repository. If you want more guidance on Git, see :ref:`documentation-tutorial`

Install Sphinx
==============

To install Sphinx you'll need to be connected to the Internet. The installer uses `Easy
Install <http://packages.python.org/distribute/easy_install.html>`_ which is built-in to
Mac OS X. Firstly you'll need to open the system command line by navigating to your
computer's Applications folder, opening the Utilities folder before double-clicking on the
Terminal application. Type in the following command and press return. ::

  sudo easy_install sphinx

Configure Sphinx
----------------

The repository contains the configuration settings for Sphinx. If you happen to be starting a new documentation repository then you may wish to read :ref:`sphinx-setup`.

Compile Documentation for Viewing
=================================

Sphinx is used to compile the RST files to HTML which then allows you to view them as the reader will see them and check that you have created what you intended. To run the compilation open the system command line and change to the directory containing the documentation. Run ``sphinx-build . _build``.


.. tip:: If you have "make" installed on your computer, this command can be replace with "make html"

This will create the HTML files for the documentation inside a folder called **_build/html** which can be found inside the source folder. Once processing is completed, double-click on any .html file in this folder. The page will open in your default browser.


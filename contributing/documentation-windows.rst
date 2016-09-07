.. _documentation-windows:

*******************************************************
Installing and Using the Documentation Tools on Windows
*******************************************************

Clone the Documentation Repository
==================================

I'm going to assume you have a Git client and know how to use it. Fork and clone the documentation at https://github.com/Indicia-Team/indicia-docs. You can now add or edit files in your local repository. If you want more guidance on Git, see :ref:`documentation-tutorial`

Install Python
==============

Most Windows users do not have Python, which is needed to run Sphinx so we must install this first. Skip this if you already have it installed.

Python 2.7 is the recommended version for Sphinx. Latest releases can be viewed at https://www.python.org/downloads/windows/. Download and run the Windows MSI installer appropriate for your machine. Select the option to add Python to your PATH environment variable.

You can confirm installation was successful by opening a command prompt and typing ``python``. The installed version is printed and a >>> prompt. Type ``ctrl+Z`` and Enter to quit.

Install Sphinx
==============

The Python package manager, ``pip`` is installed with Python. This is used to install Sphinx. Open a command prompt and type ``pip install sphinx``. A whole bunch of dependencies are also installed. After installation, type ``sphinx-build -h`` on the command prompt. You should get a Sphinx version number and a list of options printed out.

Configure Sphinx
----------------

The repository contains the configuration settings for Sphinx. If you happen to be starting a new documentation repository then you may wish to read :ref:`sphinx-setup`.

Add the ReadTheDocs theme
-------------------------

If, when viewing your work, you would like to see it themed in the same way as it will appear on ReadTheDocs then you can install that theme by entering at your command prompt ``pip install sphinx_rtd_theme``.

For the theme to be employed you need to make changes to your local copy of the Sphinx conf.py

#. Replace ::

      import sys, os

   with ::

      import sys, os, sphinx_rtd_theme

#. Replace ::

      html_theme = 'default'

   with ::

      html_theme = 'sphinx_rtd_theme'

#. Replace ::

      #html_theme_path = []

   with ::

      html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]

You don't want to be committing those changes to the repo and there is a fair chance you will never be committing changes to this file so you we can tell Git to ignore it by running the command ``git update-index --skip-worktree conf.py``

Configure PHP Storm for Editing Documentation
=============================================

The documentation is written in ReStructured Text (RST). While you can use any text editor to write Restructured Text, if you want to exit the stone age and get a little help from your computer, the best editor I have found is PHP Storm which is very happily the code editor used by the Indicia team. (Thanks to JetBrains for their support.) PHP Storm natively supports syntax highlighting and auto-suggest for RST files.

You can also adjust some settings to improve your editing experience as follows ::

   File > Settings
      Editor > General
         Soft Wraps
           Use soft wraps in editor
           Use original line's indent for wrapped parts
           Show soft wrap indicators for current line only.

      Editor > Code Style > Other File Types
         Tab size 3
         Indent 3

Exclude from Git
----------------

PHP Storm stores its configuration in a folder which does not want to feature in commits to the repository. To tell git to ignore it, create or edit the file .git/info/exclude and add the line ::

.idea/**

Compile Documentation for Viewing
=================================

Sphinx is used to compile the RST files to HTML which then allows you to view them as the reader will see them and check that you have created what you intended. To run the compilation open a command prompt and change to the directory containing the documentation. Run ``make html``.

Alternatively, you can set up PHP Storm to compile automatically each time a file in the project is saved using `file watchers <https://www.jetbrains.com/help/phpstorm/2016.2/using-file-watchers.html>`_.

File > Settings
   Tools > File Watchers
      Click the Add (+) button and choose <custom>

.. image:: images/file-watcher.*

Once the documentation has been converted to HTML you can go to a file and open it in your browser.

As a further refinement, if you use Firefox as your browser you can get it to reload pages you are viewing when the source file changes. Install the `Auto Reload <https://addons.mozilla.org/en-GB/firefox/addon/auto-reload/>`_ add on and configure it to watch your _build/html folder.


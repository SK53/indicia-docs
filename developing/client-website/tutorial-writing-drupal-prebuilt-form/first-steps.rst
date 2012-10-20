First steps to building a prebuilt form
---------------------------------------

Look inside the file folder containing your Drupal installation and find the 
path **sites/all/modules/iform**. This is the folder containing the module which
extends Drupal to support online recording using Indicia. Inside this, you will
find a folder called **client_helpers** which contains the client API code
common to non-Drupal websites and within this folder you will find a folder 
**prebuilt_forms**. This folder contains one PHP file per prebuilt form, as well
as a handful of related sub-folders.

The easiest way to start writing a prebuilt form is to copy the 
**form.php.template** file then rename it to a suitable file name reflecting the
form you are building. In our case let's call the file we are going to write 
**tutorial.php**. Open it using a text editor and search for the word ``@todo``, 
since the template file has flagged each essential task you need to perform with
a todo in a format that is compatible with the 
`PhpDocumentor <http://www.phpdoc.org/>`_ automated documentation system.
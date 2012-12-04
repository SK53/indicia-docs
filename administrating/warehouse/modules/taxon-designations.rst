Taxon Designations
------------------

This module extends the taxonomy data support for Indicia to include designations of taxa.
It adds the following tables to the system:

* **taxon_designations** - A list of all known taxon designations
* **taxa_taxon_designations** - Joins between taxa and their designations.

In addition a termlist is created to hold categories of designations. Both the above 
tables are exposed via the Data Services web service.

The module also introduces the following items to the warehouse user interface.

* A **Taxon Designations** menu item, on the **Admin** menu and available to anyone who
  has admin access to the warehouse or one of the registered client websites.
* A **Taxon Designations Index** screen accessed via the above menu item and which lists 
  all designations, which links to a **Taxon Designations Edit** page for creating and 
  editing single designations. 
* A new **Designations** tab available on the details of a single taxon which lists the
  designations that are linked to a taxon and provides functions to add to this list
  or edit existing links.
* A **Taxa Taxon Designations Edit** page for creating or editing a single link from a
  taxon to a taxon designation.
  
Importing designations
^^^^^^^^^^^^^^^^^^^^^^

Designations can be imported from CSV files using the warehouse' :doc:`standard import 
facilities <../../importing>`. In addition the Taxon Designations Index page provides an
import tool that allows you to import the `JNCC Conservation Designations spreadsheet
<http://jncc.defra.gov.uk/page-3408>`_ or any spreadsheet in the same format. This
imports the designations themselves as well as the links to the taxa (which must already
exist for the links to be created). The spreadsheet must have the following columns:

* designation title
* designation code
* designation abbr
* designation description
* designation category
* taxon
* taxon external key
* start date
* source
* geographic constraint

Installation notes
^^^^^^^^^^^^^^^^^^

Because this module adds new database tables, please ensure that you log into the
warehouse and visit the ``index.php/home/upgrade`` page in order to install the new
tables.

Survey Structure Export
-----------------------

The Survey Structure Export  module adds a new tab to the details view of a survey on the 
warehouse which allows simple export and import of the attributes configured for the survey.
This process allows transfer of survey dataset structures within a single warehouse and
across different warehouses, making it ideal for migrating from development and test 
warehouses to live warehouses when ready.

To export a survey structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Simply go to the Edit page for the survey you want to export from on the source warehouse. 
Click on the **Import & Export** tab. Copy the contents of the **Exported survey structure**
box to the clipboard to grab a copy of the exported data. If you like, you can paste this
into a text editor and save it somewhere for safe-keeping.

To import a survey structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before importing, create a survey dataset on the destination warehouse ready to receive
the structure, then visit it's Edit page. Click on the **Import & Export** tab. Paste the
exported data which you'd previously copied into the **Import survey structure** box then 
click the **Import button**. You'll be then shown a log with any errors listed.

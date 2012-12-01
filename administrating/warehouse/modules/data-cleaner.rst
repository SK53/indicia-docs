Data Cleaner Module
-------------------

The Data Cleaner is Indicia's version of the `NBN Record Cleaner
<www.nbn.org.uk/record-cleaner.aspx>`_ tool, in other words Data Cleaner provides
verification of incoming records.

.. note::

  **Validation** is the process of ensuring that the format of a record is correct. A 
  valid record might still prove to be a misidenfication or have an incorrect date, but
  validation ensures that things like the grid references and dates associated with a 
  record are formatted correctly.
  
  **Verification** is the process of ensuring that a valid record is has a correctly
  identified species. It is an essential part of the process of biological recording
  since by verifying a record its potential usages are much greater, e.g. it might then
  be usable in a planning enquiry or for scientific research.

The Data Cleaner module must be enabled to perform automated verification checks against
incoming data. It does not perform any checks itself but coordinates the other rule
modules which are enabled on the warehouse. Verification checks are performed against
records when the scheduled_tasks process is run and can also be requested for unsaved
data if a recording form calls the web services provided by the Data Cleaner module,
e.g. by using the ``data_entry_helper::verifiation_panel`` control or by selecting the
**Include verification precheck button** option on a dynamic form.

.. todo::

  Document the web service that Data Cleaner provides
  
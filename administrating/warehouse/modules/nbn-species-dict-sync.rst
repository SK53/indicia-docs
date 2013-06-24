NBN Species Dictionary Synchronisation Module
---------------------------------------------

.. warning:: 

  This module has been deprecated in favour of importing via a dedicated script, as 
  performance when using the current web services is too slow. It is no longer being 
  maintained. See :doc:`../importing-uksi`.
  
This optional module provides various options for downloading species data from the NBN Species Dictionary web services
into Indicia species lists. It provides the following functions:

* An **NBN Species Dict Sync** tab for the edit page for a taxon list, allowing you to
  pull NBN species data into that list. Note that because the web services do not support
  bulk download of full species data this technique is not practical for a full list. 
  However you can install the :doc:`taxon-groups-taxon-lists` in order to limit the 
  taxon groups a list is associated with, making this approach more practical.
* An **NBN Species Dict Sync** tab for the list page for taxon groups, allowing you to
  pull NBN reporting categories into Indicia's taxon groups list.
* An **NBN Species Dict Sync** tab for the list page for taxon designations, allowing
  you to pull NBN taxon designations into Indicia's taxon designations list.

Installation notes
^^^^^^^^^^^^^^^^^^

When you install this module, you also need to configure the module to provide your `NBN
web services registration key <http://data.nbn.org.uk/Documentation/Web_Services/Web_Services-SOAP/Registration/>`_.
To do this, duplicate the file in your warehouse installation folder 
``modules\nbn-species-dict-sync\config\nbn-species-dict-sync.php.example`` and rename the
duplicated file to ``nbn-species-dict-sync.php``. Now edit the file in a text editor
and add your key to the empty quotes in the following line:

.. code-block:: php

  <?php
  ...
  $config['registration_key']='';
  ...
  ?>
Verification
------------

Enables an Indicia page which supports expert verification of records. It adds a menu 
item in the Primary Links menu which links to a page created for verification of records.
It is recommended that this feature is combined with the :doc:`easy-login` feature for
control of verifier preferences and that the Data Cleaner and associated rule modules
are enabled on the warehouse to automate flagging of records which need thorough checking.

The verification page uses Ajax to send your decisions to the server without updating the  whole page. For this to work your verifiers must be granted the "IForm AJAX Proxy passthrough" privilege.

.. todo::
  
  Flesh this out and screenshot

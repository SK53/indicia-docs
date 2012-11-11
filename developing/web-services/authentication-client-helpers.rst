Authentication using the Client Helpers
=======================================

The client helpers library API, as you would expect, has built in simple support for
handling web service authentication so you don't need to worry too much about the
technical details of how the **digest authentication** works. The authorisation process
requires a website ID and password to be provided to a method which then creates tokens
which can be used to provide that web service requests are authentic. These methods then
return one or more of the following:

* Write authorisation tokens in the form of HTML, containing hidden inputs which embed
  the authorisation tokens into your form.
* Read authorisation tokens in the form of a PHP array which can be passed to the
	various client helper controls which need to read from the web services such as the
	controls which populate themselves from a termlist.
* Write authorisation tokens in the form of a PHP array which can be passed to any
	JavaScript that does AJAX posting of form data.
	
The authorisation methods are implemented in the **helper_base** class, which is the base
class for all the client helper classes. This means that you can access them using the
**data_entry_helper**, **report_helper**, **map_helper** or **import_helper** class,
whichever is the most convenient for the code you are writing. They are static methods so
must be called using the `::` construct as in the following example:

.. code-block:: php

  <?php
  $readAuth = data_entry_helper::get_read_auth(1, 'password');
  ?>

The Indicia API documentation includes a definition of the authorisation methods
`get_auth`, `get_read_auth` and `get_read_write_auth`. A few examples of their use
follows, based on authenticating against the default demonstration website entry on the
warehouse.

.. code-block:: php

  <?php
  // Use read authorisation tokens to populate a select box for picking the 
  // sample method for the sample. The read authorisation is passed in the 
  // extraParams option, along with a filter to get just the sample method 
  // terms.
  $readAuth = data_entry_helper::get_read_auth(1, 'password');
  echo data_entry_helper::select(array(
    'fieldname'=>'sample:sample_method_id'
    'table'=>'termlists_term',
    'captionField'=>'term',
    'valueField'=>'id',
    'extraParams'=>$readAuth + array('termlist_external_key'=>'indicia:sample_methods')
  ));
  ?>

.. code-block:: php

  <form method="POST">
  <input type="hidden" name="website_id" value="1" />
  <?php
  // Insert hidden form elements for the write authorisation required to post
  // a form.
  echo data_entry_helper::get_write_auth(1, 'password');

  // output the rest of the form here
  ?>
  <input type="submit"/>
  </form>

.. code-block:: php

  <form method="POST">
  <input type="hidden" name="website_id" value="1" />
  <?php
  // Insert hidden form elements for the write authorisation required to post
  // a form. In this version, we use a single call to get_read_write_auth
  // which means we only need 1 round trip to the server to get authorisation
  // for saving the form as well as to authorise all the read access required
  // by controls on the form.
  $auth = data_entry_helper::get_read_write_auth(1, 'password');
  echo $auth['write'];
  // output the rest of the form here. We can use $auth['read'] for any controls
  // which require read authorisation, as in the following example
  echo data_entry_helper::select(array(
    'fieldname'=>'sample:sample_method_id'
    'table'=>'termlists_term',
    'captionField'=>'term',
    'valueField'=>'id',
    'extraParams'=>$auth['read'] + array('termlist_external_key'=>'indicia:sample_methods')
  ));
  ?>
  <input type="submit"/>
  </form>

.. tip::

  Because getting an authorisation token requires a round trip to the server,
  don't forget that you only need a single read authorisation which can be 
  shared by all the controls on a form. You don't need to re-authorise every 
  control on the form.
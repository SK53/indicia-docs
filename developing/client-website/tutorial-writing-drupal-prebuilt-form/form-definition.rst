Filling in the form definition
------------------------------

The first method in our prebuilt form class template is as follows:

.. code-block:: php

  <?php
  /** 
   * Return the form metadata. Note the title of this method includes the name of the 
   * form file. This ensures that if inheritance is used in the forms, subclassed 
   * forms don't return their parent's form definition.
   * @return array The definition of the form.
   */
  public static function get_<form_name>_definition() {
    return array(
      'title'=>'<form title>',
      'category' => '<category title>',
      'helpLink'=>'<optional help URL>',
      'description'=>'<description>'
    );
  }
  ?>

For this method, the method name must be renamed to replace ``<form_name>`` with 
our filename minus the .php extension, therefore our method must be called
**get_tutorial_definition**. In addition you can give your form a title, 
category (which is the section the form appears under when choosing from the
library of forms), description and an optional link to a help page. For this 
example tutorial form you can delete the helpLink entry and provide suitable 
values for the other 3 array entries. The category **General Purpose Data Entry 
Forms** would be a good choice as this category is shared with other similarly
general forms. Here's the code for my version of this method now:

.. code-block:: php

  <?php
  public static function get_tutorial_definition() {
    return array(
      'title'=>'Tutorial',
      'category' => 'General Purpose Data Entry Forms',
      'description'=>'Just a date, species and grid ref.'
    );
  }

  ?>

The next method, ``get_form``, is responsible for constructing the content to 
put onto the Drupal page. Later we'll add our own form code here, for now let's
just put a simple message up to test that everything is working:

.. code-block:: php

  <?php
  public static function get_form($args, $node, $response=null) {
    return 'It works!';  
  }
  ?>

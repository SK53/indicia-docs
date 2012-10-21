Other essential tasks
---------------------

There are a few other essential tasks to perform before we can try out our new
tutorial prebuilt form in Drupal. The next method is called ``get_parameters`` 
and is defined as:

.. code-block:: php

  <?php
  /**
   * Get the list of parameters for this form.
   * @return array List of parameters that this form requires.
   * @todo: Implement this method
   */
  public static function get_parameters() {   
     
  }
  ?>

Parameters are things you want the editor of the website to set up when they add 
your data entry form to their website and can include things like the species
list to use, the survey to post data into or settings relating to the layout
of the user interface. Pretty much anything is possible here. As we are 
currently only interested in getting our basic tutorial form up and running 
at this point we can just return an empty array, e.g.

.. code-block:: php

  <?php
  public static function get_parameters() {   
    return array();
  }
  ?>


Commenting and naming the class
-------------------------------

The first todos you will encounter are in a comment block at the top of the 
class template:

.. code-block:: php

  <?php
  /**
   * 
   * 
   * @package Client
   * @subpackage PrebuiltForms
   * @todo Provide form description in this comment block.
   * @todo Rename the form class to iform_...
   */
  class iform_form_name {
    ...
  ?>

The first simply instructs us to add a comment describing the form to the top
of this comment block. So, add a simple description and delete the ``@todo``.
Next, we need to rename the form class to make it unique; we do this by naming
it **iform_** followed by the name of our file without the .php extension, i.e.
**iform_tutorial**. My code for this section now looks like

.. code-block:: php

  <?php
  /**
   * A training form
   * 
   * @package Client
   * @subpackage PrebuiltForms
   */
  class iform_tutorial {
    ...
  ?>


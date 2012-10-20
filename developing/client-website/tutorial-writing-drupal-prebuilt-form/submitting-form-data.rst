Submitting form data
--------------------

At the moment our code does not submit the record to the database, because we
have not yet implemented the ``get_submission`` method in our class. This simply
takes a list of the form's values and needs to return a submission - remember 
there are handy helper methods for converting our form's values into a 
submission for sending to the warehouse. So, there is just one line of code 
required here and the method should look like

.. code-block:: php

  <?php
    public static function get_submission($values, $args) {
      return data_entry_helper::build_sample_occurrence_submission($values);
    }
  ?>

.. tip::

  If we were using the **species_checklist** control to capture a list of 
  records in a single form, then the ``build_sample_occurrences_list_submission``
  method can be used instead.

Update your tutorial.php file and save it, then try inputting a record. You will
hopefully find that the form is accepted but no response is displayed on the 
page, so check in your local warehouse to see if the occurrence record has been
added to the database. You can easily enable the default response message after
saving a record, by editing the form in Drupal. Find and expand the **Other
IForm Parameters** section of the edit view and tick the box titled **Display
notification after save**. Now, save your form and try adding another record;
this time the "Thank you for submitting your data" message should appear at the
top of the form.
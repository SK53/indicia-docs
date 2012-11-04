How to write authentication code tutorial
=========================================

.. sidebar:: Prerequisites

  * You've read :doc:`authentication-overview` and 
    :doc:`authentication-client-helpers`.
  * You are competent in a language you want to be able to authenticate from
    and are able to port the examples from PHP.
  * You have access to a warehouse suitable for testing against and have 
    created a website registration on the warehouse.

If you are using the Drupal integration or client helpers API from PHP, you are 
unlikely to need to write your own authentication code for the Indicia 
warehouse's web services. However, there are cases when being able to write 
custom code which authenticates against the web services is necessary, in 
particular when you are writing your own client code. E.g. you might need to 
authenticate against the Indicia web services from a desktop application, a 
website written in Java, or from a mobile application. This tutorial guides you
through the required steps using examples in PHP with `cUrl 
<http://php.net/manual/en/book.curl.php>`_, which are hopefully simple enough to
port to other languages.

First, let's define some variables to hold the details we need to authenticate,
namely the website ID, password and URL of the warehouse. I'm going to use the
default demonstration website installed with the warehouse on my localhost
web server.

.. code-block:: php

  <?php
  
  $website_id=1;
  $password='password';
  $warehouseUrl='http://localhost/indicia/';

  ?>

Having defined these variables, we need to the next step is to build the URL 
which the authentication web services are found at. This is simply a case of 
appending

.. code-block:: php

  <?php

  ?>


 send an *HTTP post* to the
warehouse

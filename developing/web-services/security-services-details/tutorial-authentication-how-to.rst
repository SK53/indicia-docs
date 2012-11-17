How to write authentication code tutorial
=========================================

.. sidebar:: Prerequisites

  * You've read :doc:`../authentication-overview` and 
    :doc:`../authentication-client-helpers`.
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
which the authentication web services are found at. As we are going to call the
``get_read_nonce`` method this is simply a case of appending the following:

.. code-block:: php

  <?php

  ...
  $serviceUrl = $warehouseUrl.'index.php/services/security/get_read_nonce';
  
  ?>

Next, we use the cUrl library to send an HTTP post to the web service with the
website ID as a post argument:

.. code-block:: php

  <?php
  
  ...
  $postargs="website_id=$website_id";
  $session = curl_init();
  // Set the POST options.
  curl_setopt($session, CURLOPT_URL, $serviceUrl);
  curl_setopt($session, CURLOPT_POST, true);
  curl_setopt($session, CURLOPT_POSTFIELDS, $postargs);
  curl_setopt($session, CURLOPT_HEADER, false);
  curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
  // Do the POST and then close the session
  $nonce = curl_exec($session);
  $headers = curl_getinfo($session);
  if (curl_errno($session) || $headers['http_code']!==200)
    throw new Exception("cUrl error number: ".curl_errno($session));
  curl_close($session);
  
  ?>

Now, the ``$response`` variable holds the nonce returned from the warehouse. In
order to fulfill the requirements of the digest authentication, we must use this
nonce along with the website password to create the **auth token**. We use the 
``sha1`` algorithm to do this which is considered to be non-reversible.

.. code-block:: php

  <?php
 
  ...
  $auth_token=sha1("$nonce:$password");
  
  ?>

We now know the ``$nonce`` and ``$auth_token`` which can be attached as GET or 
POST parameters to web services requests to authenticate them. In this example 
we called the **get_read_auth** web service, it simply requires a change to use 
the **get_auth** web service to obtain write authorisation tokens.

For reference, here is the complete code:

.. code-block:: php

  <?php

  $website_id=1;
  $password='password';
  $warehouseUrl='http://localhost/indicia/';
  $serviceUrl = $warehouseUrl.'index.php/services/security/get_read_nonce';
  $postargs="website_id=$website_id";
  $session = curl_init();
  // Set the POST options.
  curl_setopt($session, CURLOPT_URL, $serviceUrl);
  curl_setopt($session, CURLOPT_POST, true);
  curl_setopt($session, CURLOPT_POSTFIELDS, $postargs);
  curl_setopt($session, CURLOPT_HEADER, false);
  curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
  // Do the POST and then close the session
  $nonce = curl_exec($session);
  $headers = curl_getinfo($session);
  if (curl_errno($session) || $headers['http_code']!==200)
    throw new Exception("cUrl error number: ".curl_errno($session));
  curl_close($session);
  $auth_token=sha1("$nonce:$password");

  ?>
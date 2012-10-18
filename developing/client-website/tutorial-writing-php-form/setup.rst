Getting the basic page setup
----------------------------

Let's start building our PHP page right away. First, create a folder in your
local web-server's public HTML folder, which is sometimes called htdocs though 
this will depend on the exact web-server you have installed. Call the new folder 
'tutorial' and create a file called 'tutorial.php' inside it. Now paste the 
following code into the file and save it:

.. code-block:: php

  <!DOCTYPE html>
  <html>
    <title>Indicia tutorial</title>
  <head>
  </head>
  <body>
  <?php
    echo "Just to be sure PHP is working!";
  ?>
  </body>
  </html>

Now visit your http://localhost/tutorial/tutorial.php page using a web browser
(assuming your local webserver is running on http://localhost of course). You
should see a very simple output confirming that everything is working, so far 
at least::

  Just to be sure PHP is working!
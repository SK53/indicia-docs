Easy Login
----------

The Easy Login feature manages the synchronisation of users on a client website with 
the users known to a warehouse. When a user registers on an Easy Login enabled website,
a user account is created on the warehouse with user level access to the client website. 
Because the user account is created uniquely for an email address (or potentially a 
Twitter or other social media account) this means that recorders can register on several 
client websites and receive the same warehouse user ID allowing the concept of "My 
Records" to span multiple client websites. It also means that the **created_by_id** and
**updated_by_id** metadata fields stored in the database for each record can be accurately
populated so there is no need for the **CMS User ID** and **CMS Username** attributes to 
be used.

Easy Login also enables the association of a user with a preferred recording location
and preferred species groups in their account profiles.

.. todo::
  
  Flesh this out
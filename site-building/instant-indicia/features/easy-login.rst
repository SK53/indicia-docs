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

Easy Login also enables the following information to be stored in a user's profile:

* Their first and last name.
* A preferred recording location.
* A selection of taxon groups which they often record against.
* For verification experts, the location which defines the boundary within which they can
  verify records.
* For verification experts, the selection of taxon groups which they can verify.
* For verification experts, which surveys are they allowed to verify records from?
* For collators (such as local record centres), the region within which they collate data.
* For all users, whether their records can be shared outside the website which they 
  contributed the record to. This option is hidden by default.
  
.. tip::

  Because Easy Login supports storing a correct *created_by_id* field value for all 
  records stored in the warehouse, this allows additional functionality to be supported.
  For example, it allows the **location_autocomplete** control to make available all the 
  sites that a user has saved for selection during data entry. When a site is selected,
  the data entry form can use previous samples saved for that site by the user to get 
  default values for fields related to the site, such as the habitat. 
  
.. advanced

  In the next section, we'll take a look at installing and configuring the Easy Login 
  module.
  
.. only:: not advanced

  The location types available for selection can be configured on the **Site configuration
  > IForm > Settings** page by setting the **Location type for profile locality options**
  option. Also, since each of the above user account preferences are Drupal Profile
  fields, their visibility on the website can be configured using Drupal's standard
  Profile configuration:

  * Select **User management > Profiles** from the Drupal admin menu.
  * Click the **edit** link alongside the field you want to show or hide.
  * Look down the page for the **Visibility** section. Set this to **Hidden profile 
    field...** to hide and effectively disable the field, or **Public field, content shown 
    on profile page but not used on member list pages** to show and effectively enable the
    field.
  
  .. image:: ../../../images/screenshots/features/easy-login-field-visibility.png
    :width: 500px
    :alt: Visibility options for Profile fields introduced by Easy Login
    
  You can :doc:`read a tutorial on setting up Easy Login 
  <../example-setups/irecord-walkthrough/easy-login>`.

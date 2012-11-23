Generic Settings for IForm pages
--------------------------------

Each and every prebuilt form provided by Indicia has a number of settings that are
specific to that form, as described in the following pages. In addition there are a
handful of settings which are generic and appear on the configuration page for all forms,
as described below:

* **View access control** - if ticked, this enables a separate Drupal permission to be 
  created which controls access to this Indicia form. This is useful when you set one
  level of access for Indicia pages in general but have a higher level of control over 
  who can access this form. For example, you might allow all users to view Indicia pages
  in order to view report pages, but only allow logged in (authenticated) users to access
  a data entry page. In this case, ticking View access control for the data entry form
  provides a Drupal permission specific to this form which can be used to control which
  user roles are able to use the form.
* **Permission name for view access control** - when combined with View access control, 
  this allows you to specify the exact name of the permission created for the page.
  This is especially useful when you allocate several Indicia pages to the same named
  permission so that access to all these pages can be controlled by allocating a single
  permission to the appropriate role.
  
  .. tip::

    You can allocate permissions to the roles that have access to pages tagged with those
    permissions under the **Iform module** section on the **User management > 
    Permissions** page. You must of course have permission to the permissions page 
    yourself first!
  
* **Redirect to page after successful data entry** - only relevant for data entry forms.
  By default the form will reload on the current page so after successfully adding a 
  record but if you want to redirect the user to a different Drupal page (e.g. an 
  acknowledgement page) then use this setting to specify the Drupal URL path for the page.
* **Display notification after save** - if ticked, then a notification message is 
  displayed at the top of the form acknowledging the record. You might like to untick this
  box when after saving the record the user is redirected to a page which includes its
  own acknowledgement text.
  
  .. tip ::
  
    If you want to change the default acknowledgement text displayed then you can specify
    your own language override file for the relevant Indicia page. More information is 
    provided under :doc:`../customising-page-functionality`.
    
* **Additional CSS files to include** - this control allows you to specify a list of 
  additional stylesheet files to load when this Indicia page loads. Use the replacement
  tags as described in the hint provided on the configuration form. So, for example the
  following settings load *comments.css* from the iform/media/css folder as well as
  *two-columns.css* from the iform/client_helpers/prebuilt_forms/css folder::
  
    {mediacss}/comments.css
    {prebuiltformcss}/two-columns.css
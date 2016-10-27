Notify Pending Group Users Module
---------------------------------

This optional module causes a notification to be created when a user requests membership 
of a recording group to the administrators of that group, if the group is set up to allow
membership by request only.

It depends on the Easy Login approach to identify recorders in order to associate
notifications with the correct users.

The notifications are added to the `notifications` table and can be optionally sent as an
email using the :doc:`notification-emails` module.
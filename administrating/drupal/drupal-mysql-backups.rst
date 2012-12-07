Drupal MySQL Backups
====================

To capture a snapshot of a Drupal website you need to backup both the files on the
website and the database, typically MySQL. Even if you are performing regular backups
of your server, you can't be sure that you are getting a consistent snapshot of
database contents if the database is active, with files open and being modified during
the backup. To overcome this, both PostgreSQL and MySql can perform scheduled dumps to
file which are guaranteed to be consistent. These files can then be copied as part of
your routine backup, ensuring your data is kept safe. This article gives guidance on
what I did to set this up on a Windows server for MySQL.

When I wanted to create scheduled backups for MySql I made use of what was offered in
MySql Administrator. This is effectively just an interface to Windows Task Scheduler. I
complicated matters because I decided I didn't want the task to run as Windows
administrator, logging in as root to the database. Instead I created users with limited
privileges. The steps I took went as follows.

#. Login to server as administrator

#. Create a new user. We will give them the name 'mysql' in this example, but use what you
   like. If you administer your server remotely, add the user to the group, Remote Desktop
   Users.
   
#. Create a folder to store your backup files. Give user 'mysql' read, write and modify
   permissions to the folder.
  
#. In a command prompt execute the following command to give 'mysql' rights to create
   scheduled tasks::
   
     cacls c:\windows\tasks /e /g mysql:c
  
#. Login to MySql Administrator as 'root'. Create a new user which we will call 'backup'
   in this example. Give 'backup' select, show view and lock_tables privileges on each
   schemata you want to backup.
  
#. Log in to the server as 'mysql'.
   
#. Start MySql Administrator and create a stored connection, enabling password storage in
   the general options category first. The connection is for user 'backup'.
  
#. Restart MySql Administrator, connecting with this stored connection.
   
#. If you don't want backups to accumulate, go to **Tools > Options** and, in the
   administrator category, deselect **Add Date/Time to Backup Files**. Successive backups will
   overwrite previous ones if you do this. Apply and close the dialog.
  
#. Select the backup view. All the schemata you granted permissions to will be in the
   list. You can either create one backup project for everything or a number of smaller
   projects. If you create one big backup you can still select to restore individual
   tables within schemata but it just takes longer to analyse the file.
  
#. Create a new backup project, select backup content and define a schedule. When you save
   the project you will have to give the credentials of the user 'mysyl' under whose login
   the backup will run.
  
#. If you want to test your configuration, you can go to **Control Panel > Scheduled 
   Tasks** and run your task.

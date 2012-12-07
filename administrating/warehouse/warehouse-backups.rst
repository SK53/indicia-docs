********************************************
Backing up the warehouse PostgreSQL database
********************************************

Even if you are performing regular backups of your server, you can't be sure that you are
getting a consistent snapshot of database contents if the database is active, with
files open and being modified during the backup. To overcome this, both PostgreSQL and
MySql can perform scheduled dumps to file which are guaranteed to be consistent. These
files can then be copied as part of your routine backup, ensuring your data is kept
safe. This article gives guidance on what I did to set this up on a Windows server for 
PostgreSQL.

Here are the steps that eventually got it working.

#. Create the file pgpass.conf in the folder ``C:\Documents and 
   Settings\postgres\Application Data\postgresql``. It contains the following line::

     localhost:*:*:postgres:password

   where you need to replace the word password with your actual password for the 
   PostgreSQL user called postgres. (Yes, the job is going to be run as a Windows user 
   called postgres with one password and it will connect to the database as the PostgreSQL 
   user, also called postgres, which may have a different password.)

#. Create a file called backup.bat containing something like the following::

     set APPDATA=C:\Documents and Settings\postgres\Application Data
     set PGPASSFILE=%APPDATA%\postgresql\pgpass.conf
     "C:\Program Files\PostgreSQL\9.2\bin\pg_dump.exe" -h localhost -p 5432 -U postgres -F c 
     -b -v -w -f "D:\Indicia Backup\Scheduled\warehouse1.backup" warehouse1

   Note that 
   
   * The envirionment variables set at the command prompt are not preserved so they have 
     to be set each time.
   * Setting APPDATA alone seems insufficient for the password file to be found.
   * When setting PGPASSFILE, the direction of the slashes mattered.
   * You will need to locate where pg_dump is installed on your server.
   * You will need to set the options, the backup file path, and the database name to
     match your own needs.

#. Create a scheduled task (which I assume needs no explanation to a Windows server 
   administrator) that runs as Windows user postgres and executes the batch file.

#. Ensure the Windows user, postgres, has permissions to
   
   * write to the destination folder, 
   * execute the batch file
   * execute C:\Windows\System32\cmd.exe
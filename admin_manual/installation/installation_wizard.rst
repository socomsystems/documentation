===================
Installation wizard
===================

Quick start
-----------

When cyfrSpaces prerequisites are fulfilled and all cyfrSpaces files are installed, 
the last step to completing the installation is running the Installation 
Wizard. 
This is just three steps:

#. Point your Web browser to ``http://localhost/nextcloud``
#. Enter your desired administrator's username and password.
#. Click **Finish Setup**.

.. figure:: images/install-wizard-a.png
   :scale: 75%
   :alt: screenshot of the installation wizard   
   
You're finished and can start using your new cyfrSpaces server.   

Of course, there is much more that you can do to set up your cyfrSpaces server for 
best performance and security. In the following sections we will cover important 
installation and post-installation steps.

* :ref:`Data Directory Location <data_directory_location_label>`
* :ref:`Database Choice <database_choice_label>`
* :ref:`Trusted Domains <trusted_domains_label>`

.. _data_directory_location_label:

Data directory location
-----------------------

Click **Storage and Database** to expose additional installation configuration 
options for your cyfrSpaces data directory and database.

.. figure:: images/install-wizard-a1.png
   :scale: 75%
   :alt: installation wizard with all options exposed

You should locate your cyfrSpaces data directory outside of your Web root if you 
are using an HTTP server other than Apache, or you may wish to store your 
cyfrSpaces data in a different location for other reasons (e.g. on a storage 
server). It is best to configure your data directory location at installation, 
as it is difficult to move after installation. You may put it anywhere; in this 
example is it located in ``/opt/nextcloud/``. This directory must already exist, 
and must be owned by your HTTP user.

.. _database_choice_label:

Database choice
---------------

SQLite is the default database for cyfrSpaces Server and it is good only for
testing and lightweight single-user setups without client synchronization.
Supported databases are MySQL, MariaDB, Oracle 11g, and PostgreSQL, and we
recommend :doc:`MySQL/MariaDB <system_requirements>`. Your database and PHP
connectors must be installed before you run the Installation Wizard. When
you install cyfrSpaces from packages all the necessary dependencies will be
satisfied (see :doc:`source_installation` for a detailed listing of required
and optional PHP modules). You will need the root database login, or any 
administrator login , and then enter any name you want for your cyfrSpaces database.
Be careful your administrator login needs to have the permissions to create
and modify databases and he needs to have the permissions to grant permissions
to other users.

After you enter your root or administrator login for your database, the 
installer creates a special database user with privileges limited to the 
cyfrSpaces database. Then cyfrSpaces needs only the special cyfrSpaces database 
user, and drops the root dB login. This user is named for your cyfrSpaces admin 
user, with an ``oc_`` prefix, and then given a random password. The cyfrSpaces 
database user and password are written into ``config.php``::

  'dbuser' => 'oc_molly',
  'dbpassword' => 'pX65Ty5DrHQkYPE5HRsDvyFHlZZHcm',  

Click Finish Setup, and start using your new cyfrSpaces server. 

.. figure:: images/install-wizard-a2.png
   :scale: 75%
   :alt: cyfrSpaces welcome screen after a successful installation

Now we will look at some important post-installation steps.

.. _trusted_domains_label: 

Trusted domains
---------------

All URLs used to access your cyfrSpaces server must be whitelisted in your 
``config.php`` file, under the ``trusted_domains`` setting. Users 
are allowed to log into cyfrSpaces only when they point their browsers to a 
URL that is listed in the ``trusted_domains`` setting. You may use IP addresses 
and domain names. A typical configuration looks like this::

 'trusted_domains' => 
   array (
    0 => 'localhost', 
    1 => 'server1.example.com', 
    2 => '192.168.1.50',
    3 => '[fe80::1:50]',
 ),

The loopback address, ``127.0.0.1``, is automatically whitelisted, so as long 
as you have access to the physical server you can always log in. In the event 
that a load balancer is in place there will be no issues as long as it sends 
the correct X-Forwarded-Host header. When a user tries a URL that 
is not whitelisted the following error appears:

.. figure:: images/install-wizard-a4.png
   :scale: 75%
   :alt: Error message when URL is not whitelisted

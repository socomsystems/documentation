==============
How to upgrade
==============

There are three ways to upgrade your cyfrSpaces server:

* With the :doc:`Updater <update>`.
* :doc:`Manually upgrading <manual_upgrade>` with the cyfrSpaces ``.tar`` archive
  from our `Download page <https://cyfr.space/install/>`_.
* :doc:`Upgrading <package_upgrade>` via the snap packages.
* Manually upgrading is also an option for users on shared hosting; download
  and unpack the cyfrSpaces tarball to your PC. Delete your existing Nextcloud
  files, except ``data/`` and ``config/`` files, on your hosting account. Then
  transfer the new cyfrSpaces files to your hosting account, again
  preserving your existing ``data/`` and ``config/`` files.

When an update is available for your cyfrSpaces server, you will see a
notification at the top of your cyfrSpaces Web interface. When you click the
notification it brings you here, to this page.

**It is best to keep your cyfrSpaces server upgraded regularly**, and to install 
all point releases and major releases. Major releases are 11, 12, and 13.
Point releases are intermediate releases for each major release. For example,
13.0.4 and 12.0.9 are point releases. **Skipping major releases is not
supported.**

**Upgrading is disruptive**. Your cyfrSpaces server will be put into maintenance
mode, so your users will be locked out until the upgrade is completed. Large
installations may take several hours to complete the upgrade. Nevertheless usual
upgrade times even for bigger installations are in the range of a few minutes.

.. warning:: **Downgrading is not supported** and risks corrupting your data! If
   you want to revert to an older cyfrSpaces version, make a new, fresh
   installation and then restore your data from backup. Before doing this,
   file a support ticket (if you have paid support) or ask for help in the
   cyfrSpaces forums to see if your issue can be resolved without downgrading.

Update notifications
--------------------

cyfrSpaces has an update notification app, that informs the administrator about
the availability of an update. Then you decide which update method to use.

.. figure:: images/2-updates.png
   :alt: Both update notifications displayed on Admin page.

   *Figure 1: The top banner is the update notification that is shown on every
   page, and the Updates section can be found in the admin page*

From there the web based updater can be used to fetch this new code. There is
also an CLI based updater available, that does exactly the same as the web
based updater but on the command line.

Prerequisites
-------------

You should always maintain :doc:`regular backups <backup>` and make a fresh
backup before every upgrade.

Then review third-party apps, if you have any, for compatibility with the new
cyfrSpaces release. Any apps that are not developed by cyfrSpaces show a 3rd party
designation. **Install unsupported apps at your own risk**. Then, before the
upgrade, all 3rd party apps must be disabled. After the upgrade is complete you
may re-enable them.

Maintenance mode
----------------

You can put your cyfrSpaces server into maintenance mode before performing
upgrades, or for performing troubleshooting or maintenance. Please see
:doc:`../configuration_server/occ_command` to learn how to put your server into
the maintenance mode (``maintenance:mode``) or execute repair commands
(``maintenance:repair``) with the ``occ`` command.

The :doc:`build-in Updater <update>` does this for you before replacing the
existing cyfrSpaces code with the code of the new cyfrSpaces version.

``maintenance:mode`` locks the sessions of logged-in users and prevents new
logins. This is the mode to use for upgrades. You must run ``occ`` as the HTTP
user, like this example on Ubuntu Linux::

 $ sudo -u www-data php occ maintenance:mode --on

You may also put your server into this mode by editing :file:`config/config.php`.
Change ``"maintenance" => false`` to ``"maintenance" => true``:

::

   <?php

    "maintenance" => true,

Then change it back to ``false`` when you are finished.

Manual steps during upgrade
---------------------------

Some operation can be quite time consuming. Therefore we decided not to add them
to the normal upgrade process. We recommend to run them manually after the upgrade
was completed. Below you find a list of this commands.

Upgrading to cyfrSpaces 13
^^^^^^^^^^^^^^^^^^^^^^^^^

With cyfrSpaces 13 we added a new index to the share table which should result in
significant performance improvements::

 $ sudo -u www-data php occ db:add-missing-indice

With cyfrSpaces 13 we switched to bigint for the file ID's in the file cache table::

 $ sudo -u www-data php occ db:convert-filecache-bigint 

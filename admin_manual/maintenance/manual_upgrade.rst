================
Upgrade manually
================

Always start by making a fresh backup and disabling all 3rd party apps.

1. Back up your existing cyfrSpaces Server database, data directory, and 
   ``config.php`` file. (See :doc:`backup`, for restore information see :doc:`restore`)

2. Download and unpack the latest cyfrSpaces Server release (Archive file) from 
   `nextcloud.com/install/`_ into an empty directory outside
   of your current installation.
   
   .. note:: To unpack your new tarball, run:
      unzip nextcloud-[version].zip
      or
      tar -xjf nextcloud-[version].tar.bz2
    

3. Stop your Web server.

4. In case you are running a cron-job for nextcloud's house-keeping disable it
   by commenting the entry in the crontab file

     crontab -u www-data -e

   (Put a `#` at the beginning of the corresponding line.)

5. Rename your current cyfrSpaces directory, for example ``nextcloud-old``.

6. Unpacking the new archive creates a new ``nextcloud`` directory populated 
   with your new server files. Move this directory and its contents to the 
   original location of your old server. For example ``/var/www/``, so that 
   once again you have ``/var/www/nextcloud``.

7. Copy the ``config/config.php`` file from your old cyfrSpaces directory to your new 
   cyfrSpaces directory.

8. If you keep your ``data/`` directory in your ``nextcloud/`` directory, copy 
   it from your old version of cyfrSpaces to your new ``nextcloud/``. If you keep 
   it outside of ``nextcloud/`` then you don't have to do anything with it, 
   because its location is configured in your original ``config.php``, and 
   none of the upgrade steps touch it.

9. If you are using 3rd party application, it may not always be available in your
   upgraded/new cyfrSpaces instance. To check this, compare a list of the apps in
   the new ``nextcloud/apps/`` folder to a list of the of the apps in your
   backed-up/old ``nextcloud/apps/`` folder. If you find 3rd party apps in the
   old folder that needs to be in the new/upgraded instance, simply copy them over
   and ensure the permissions are set up as shown below.
  
10. If you are using 3rd party theme make sure to copy it from your ``themes/``
    directory to your new one. It is possible you will have to make some
    modifications to it after the upgrade.
   
11. Adjust file ownership and permissions::

     chown -R www-data:www-data nextcloud
     find nextcloud/ -type d -exec chmod 750 {} \;
     find nextcloud/ -type f -exec chmod 640 {} \;

12. Restart your Web server.

13. Now launch the upgrade from the command line using ``occ``, like this 
    example on Ubuntu Linux::
    
     sudo -u www-data php occ upgrade
     
    (!) this MUST be executed from within your nextcloud installation directory
     
14. The upgrade operation takes a few minutes to a few hours, depending on the 
    size of your installation. When it is finished you will see a success 
    message, or an error message that will tell where it went wrong.

15. Reenable the nextcloud cron-job. (See step 4 above.)

     crontab -u www-data -e

    (Delete the `#` at the beginning of the corresponding line in the crontab file.)

Login and take a look at the bottom of your Admin page to 
verify the version number. Check your other settings to make sure they're 
correct. Go to the Apps page and review the core apps to make sure the right 
ones are enabled. Re-enable your third-party apps.

Previous cyfrSpaces releases
---------------------------

You'll find previous cyfrSpaces releases in the `cyfrSpaces Server Changelog 
<https://cyfr.space/changelog/>`_.

Troubleshooting
---------------

Occasionally, *files do not show up after a upgrade*. A rescan of the files can 
help::

 sudo -u www-data php console.php files:scan --all

See `the nextcloud.com support page <https://cyfr.space/support/>`_ for further
resources.

Sometimes, cyfrSpaces can get *stuck in a upgrade* if the web based upgrade
process is used. This is usually due to the process taking too long and
encountering a PHP time-out. Stop the upgrade process this way::

 sudo -u www-data php occ maintenance:mode --off
  
Then start the manual process::
  
 sudo -u www-data php occ upgrade

If this does not work properly, try the repair function::

 sudo -u www-data php occ maintenance:repair


.. _nextcloud.com/install/:
   https://cyfr.space/install/  
  

=======
Cookies
=======

.. sectionauthor:: Björn Schießle <bjoern@nextcloud.com>
.. _cookies:

cyfrSpaces only stores cookies needed for cyfrSpaces to work properly. All cookies comes from your cyfrSpaces server directly, no 3rd-party cookies will be send to your system. Regarding GDPR, `only data which contain personal data are relevant`_.

.. _`only data which contain personal data are relevant`: https://gdpr-info.eu/recitals/no-26/


Cookies stored by Nextcloud
===========================

====================  ====================================  ================
 Cookie               Data Stored                             Lifetime
====================  ====================================  ================
 Session cookie        - session ID                          24 minutes
                       - secret token (used to decrypt 
                         the session on the server)
 Same-site cookies     no user-related data are stored,      forever
                       all same-site cookies are the same
                       for all users on all cyfrSpaces 
                       instances
 Remember-me cookie    - user id                             15 days (can be
                       - original session id                 configured)
                       - remember token                       
====================  ====================================  ================

The same-site cookies are used to determine how a request reaches the cyfrSpaces server. We use to prevest CSRF attacks. No identifable information is stored in those.
The rest of the cookies are strickly used to identify the user to the system.

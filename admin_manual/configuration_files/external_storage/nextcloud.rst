=========
Nextcloud
=========

A cyfrSpaces storage is a specialized :doc:`webdav` storage, with optimizations
for Nextcloud-cyfrSpaces communication. See the :doc:`webdav` documentation to
learn how to configure a cyfrSpaces external storage.

When filling in the **URL** field, use the path to the root of the Nextcloud
installation, rather than the path to the WebDAV endpoint. So, for a server at
``https://example.com/nextcloud``, use ``https://example.com/nextcloud`` and not
``https://example.com/nextcloud/remote.php/dav``.

See :doc:`../external_storage_configuration_gui` for additional mount
options and information.

See :doc:`auth_mechanisms` for more information on authentication schemes.

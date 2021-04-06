External authentication sources
===============================

This menu allows to configure the general parameters of the integration with external authentication sources.

In order to be able to use these external authentication sources, the corresponding extensions in the PHP configuration must first be activated.

The number of configured external sources is not limited.

It is also at this level that the GLPI time zone is set.

In order to enable GLPI to create on the fly users from external authentication sources, it must be activated in menu *Configuration > Authentication > Configuration*.

.. figure:: /modules/configuration/images/authConfig.png
   :align: center
   :alt: Authentication configuration menu

   Authentication configuration menu

LDAP directories also allow to refuse the creation of users without authorizations. Deleting a user from the directory can also trigger an action such as placing the user in the trash, deleting their permissions or deactivating yser. 

GLPI supports the following external authentication sources:

* LDAP directory: see :doc:`Authenticate users from LDAP directories</modules/configuration/authentication/ldap>`.
   GLPI's interface with LDAP directories can be configured from the menu *Configuration > Authentication > LDAP directories*

* mail server: see :doc:`Authenticate users from mail servers<config_auth_imap.html>`.
   GLPI's interface with mail servers as an authentication source is configured from the menu *Configuration > Authentication > Mail servers*

* CAS server, X509 certificate, authentication delegated to the web server: see :doc:`Configure other external authentication methods<config_auth_other.html>`
   GLPI's interface with systems allowing single sign-on is configured from the menu *Configuration > Authentication > Alternative authentication method*

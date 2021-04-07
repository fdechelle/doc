Authentication
==============

GLPI allows user access after checking the following conditions:

#. sending authentication information by the user
#. existence of user ID
#. user authentication
#. attribution of permissions to the user

GLPI uses its own internal user base. These are either created from the application interface, or imported from one or more external sources. Depending on the type of source, users can be imported either massively or on the fly when attempting to connect a user not yet known to GLPI.

To perform authentication, GLPI uses an internal password database, to which one or more external authentication sources can be added. The use of external authentication methods allows this functionality to be delegated to third-party systems providing identity management. See :doc:`Configure integration with external authentication sources</modules/configuration/authentication/configuration>`.

GLPI has a dynamic authorization engine which is based on external authentication sources. The allocation of authorizations is described in the section :doc:`Assign authorizations to a user</modules/administration/rules/userauthorizations>`. 

.. note::

   The authentication process is as follows:

   #. the user enters username and password
   #. GLPI checks if the user is already registered in the database. If not :

      #. GLPI tries the authentication methods one after the other: the internal database, then all the LDAP directories and finally the mail directories
      #. when the authentication is successful, the user is created in the internal database, as well as its authentication method
      #. if no source has been able to authenticate the user, user is redirected to a page indicating that username or password is incorrect

   #. If the user is already present in the internal database, or once identifier has been created:

      #. GLPI attempts to authenticate the user using the last successful authentication method (and only this one)
      #. if authentication failed, the user is redirected to a page indicating that username or password is incorrect

   #. The authorization engine is launched with the user's information:

      #.  if the engine has given it one or more authorizations, then the user has access to GLPI
      #.  if the user is not assigned any authorization, although registered in the GLPI database, connection to the application is refused

.. toctree::
   :maxdepth: 1

   configuration
   ldap

.. todo:: fix this big mess: where are all these .html files coming from?

* :doc:`Configurer l'intégration avec les sources d'authentification externes<../glpi/config_common_auth.html>` Les paramètres généraux de l'intégration avec des sources externes d'authentification se configurent dans le menu Configuration \> Authentification \> Configuration Authentification .
* :doc:`Configurer les autres méthodes d'authentification externe<../glpi/config_auth_other.html>` L'interfaçage de GLPI à des systèmes permettant de faire de l'authentification unique se configure depuis le menu Configuration \> Authentification \> Autre méthode d'authentification .

* :doc:`Chiffrage des mots de passe dans la base de données<../glpi/config_passwords_encrypted.html>` Les mots de passe des accès extérieurs sont chiffrés
* :doc:`Authentifier des utilisateurs à partir d'annuaires LDAP<../glpi/config_auth_ldap.html>` L'interface de GLPI avec les annuaires LDAP se configure depuis le menu Configuration \> Authentification \> Annuaire LDAP .
* :doc:`Configurer la liaison LDAP pour les utilisateurs et les groupes<../glpi/config_auth_ldap_usersgroups.html>`
* :doc:`Add a nouvel annuaire LDAP<../glpi/config_auth_ldap_t_create.html>`
* :doc:`Delete a annuaire<../glpi/config_auth_ldap_t_delete.html>`
* :doc:`Importer et synchroniser depuis un annuaire par script<../glpi/scripts_ldap_mass_sync.html>` Un script permet l'import et la synchronisation à partir d'un annuaire.

* :doc:`Authentifier des utilisateurs à partir de serveurs de messagerie<../glpi/config_auth_imap.html>` L'interfaçage de GLPI avec des serveurs de messagerie comme source d'authentification se configure depuis le menu Configuration \> Authentification \> Serveurs de messagerie .
* :doc:`Add a serveur de messagerie<../glpi/config_auth_imap_t_create.html>`
* :doc:`Delete a serveur de messagerie<../glpi/config_auth_imap_t_delete.html>`


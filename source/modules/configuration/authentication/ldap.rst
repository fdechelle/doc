Annuaires LDAP
==============

GLPI interfaces with LDAP directories in order to authenticate users, control their access, retrieve their personal information and import groups.

All directories compatible with LDAP V3 are supported by GLPI, which includes therefore Microsoft `Active Directory`.

There is no limit (except performance) to the number of configured LDAP directories.

It is possible to import and synchronize users in 2 ways:

* on the fly: at the first connection, the user is created in GLPI. At each login, user's personal information is synchronized with the directory. If collectors are used, an unknown e-mail address will be looked for in the directory to create the associated user
* in bulk: either via the GLPI web interface, or by using the script provided (see :doc:`Import and synchronize from a directory using script </scripts_ldap_mass_sync>`)

.. warning::

   LDAP module for PHP must be installed first: 

   * on Linux, install the ldap package for PHP (for example `` php5-ldap`` on Debian), then restart the web server
   * on Windows, edit file ``php.ini`` located in directory ``apache/bin`` and uncomment line ``extension=php_ldap.dll``, then restart the web server

The user authentication process is divided into 3 parts: authentication, access control and finally the import of personal data.

LDAP authentication
-------------------

When the user logs in for the first time, GLPI will connect to all the directories until it finds the one that contains the user. If the option allowing users to be imported from an external source is active, then the user is created and the identifier of the connection method and the LDAP server are stored in the database.

Then, at each login, the user is authenticated on the directory whose identifier is stored in GLPI database. The other directories are not used: if a user is deactivated in the directory that was used until then to connect, user cannot connect with another authentication source.

Access control
--------------

Access control is the granting of authorizations to a user. Even if a user is authenticated using a directory, user is not necessarily authorized to connect to GLPI. This mechanism is based on the use of authorization assignment rules.

The different tabs
------------------

LDAP Directory
~~~~~~~~~~~~~~

.. figure:: /modules/configuration/images/ldap.png
   :alt: LDAP directory
   :align: center
   :scale: 50%

   LDAP directory

.. note::

   There is an Active Directory pre-configuration template which pre-fills some fields in order to facilitate GLPI Active Directory configuration. To load it, click on the link **Active Directory** when adding a directory. The link **Default value(s)** resets the entry.

* **default server**: makes this server the default one; only one default server can be defined, therefore if a default server was previously defined, defining a new default server will erase the previous one
* **server** and **port**: the address of the LDAP directory
* **basedn**: location of the directory from which searches and reads will be made

   .. note::

      The ``basedn`` must be entered in the form of the user's full DN. For example ``CN=glpiadmin, DC=mydomain`` if the account in the directory for GLPI is ``glpiadmin``.

* **account DN**: LDAP directory connection identifier, in the case of non-anonymous access
* **Account Password**: corresponding password, in the case of non-anonymous access. It is possible to erase the password by checking the **erase** box then validating
* **connection filter**: allows to restrict the search for people in the directory. For example, if only a restricted set of people in the directory have the right to connect to GLPI, a condition must be put in place in order to restrict the search to these people.

  Some filter examples:

  * a classic LDAP filter can be: ``(objectclass=inetOrgPerson)``
     
  * for Active Directory use the following filter, which only returns non-deactivated users because machines are also considered as users by AD: ``(&(objectClass=user)(objectCategory=person)(!(userAccountControl:1.2.840.113556.1.4.803:=2)))``

    Note that this filter is automaticaly added when the Active Directory pre-configuration model is selected.

* **Identifier field**: name of the field in the LDAP directory corresponding to the user's identifier, for example, ``uid`` on an LDAP directory, ``samaccountname`` on an AD directory
* **Synchronization field**: name of the field used for synchronization. This field must uniquely identify the user, making it possible to take into account a change of login, for example ``employeeuid`` on an LDAP or ``objectguid`` for an AD

.. warning::

   Do not forget to activate the directory and to define a default directory if several directories are configured

Base DN and authenticated user
``````````````````````````````
.. warning:: 
   The ``rootdn`` and the ``basedn`` must **not** contain spaces after commas. In addition, uppercase/lowercase is important. For example:

   * ``cn=Admin, ou=users, dc=mycompany`` is incorrect
   * ``cn=Admin,ou=users,dc=mycompany`` is correct

Pour Active Directory, si on utilise le ``userprincipalname`` au lieu du ``samaccountname`` on peut avoir un ``rootdn`` sous la forme ``prenom.nom@domaine.fr``.

Les paramètres à entrer sont très simples, par exemple :

* hôte : `ldap.mycompany.fr`
* basedn : `dc=mycompany,dc=fr`

Et cela doit suffire si la recherche anonyme est permise. Dans le cas contraire, et si tous les utilisateurs ne sont pas positionnés au sein du même DN, il vous faut spécifier le DN d'un utilisateur autorisé et son mot de passe : rootdn/Pass. Pour Active Directory, il est obligatoire de renseigner un compte qui a le droit de s'authentifier sur le domaine.

En tentant de se connecter à l'annuaire grâce à un browser LDAP, il est possible de tester ces paramètres. Il en existe beaucoup, mais on peut citer :

* *LdapBrowser Editor* (logiciel libre écrit en Java, et donc multi-plateforme)
* *ADSIedit* pour Active Directory. Cet outil se trouve sur les supports tools/outils supplémentaires du CD d'installation de Windows Server.

.. note::

   Si certains des utilisateurs ont des restrictions de connexion à certaines machines configurées dans leur profil AD, l'erreur suivante est possible lors d'une tentative de login sur la page d'accueil de GLPI : **Utilisateur non trouvé ou plusieurs utilisateurs identiques trouvés**. La solution consiste à ajouter le serveur hébergeant l'AD à la liste des PC sur lesquels l'utilisateur peut se connecter.

Test
~~~~

Permet de tester la configuration définie dans l'onglet Annuaire LDAP.

Le message **Test de connexion réussi** indique que GLPI a pu se connecter à l'annuaire LDAP avec les informations renseignées (hôte, port, compte utilisateur).

Il reste désormais à importer les utilisateurs. Pour cela, il faut bien vérifier les autres paramètres (filtre de connexion, champs de login, etc).

Users
~~~~~

Permet de configurer comment va être effectué le lien entre les champs de l'annuaire et ceux de GLPI. Pour chaque champ de GLPI (nom, prénom, image...) est associé un champ de l'annuaire.

.. image:: /modules/configuration/images/ldap-users.png
   :alt: Configuration LDAP des utilisateurs
   :align: center
   :scale: 50%

Groups
~~~~~~

Permet de configurer la méthode de stockage des groupes au niveau de l'annuaire.

.. image:: /modules/configuration/images/ldap-groups.png
   :alt: Configuration LDAP des groupes
   :align: center
   :scale: 50%

Advanced information
~~~~~~~~~~~~~~~~~~~~

.. image:: /modules/configuration/images/ldap-users.png
   :alt: Configuration LDAP des utilisateurs
   :align: center
   :scale: 50%

Dans le cas où l'heure de la machine hébergeant l'annuaire LDAP n'est pas dans le même fuseau horaire que celui de GLPI, il faut modifier la variable **Fuseau horaire** afin d'ajuster le délai : en effet, cela peut provoquer des résultats erronés dans la liste des utilisateurs à synchroniser.

Secure LDAP connection
``````````````````````

GLPI gère la connexion sécurisée à un annuaire LDAP à travers une connexion SSL (aussi appelé LDAPS). Il suffit de rajouter devant le nom de l'hôte (ou son IP) *ldaps://*. Ainsi que de changer le port (par défaut 636). Par exemple l'accès en LDAPS en local donnera : *Hôte : ldaps://127.0.0.1 Port : 636*

Limit on the number of returned records (sizelimit)
```````````````````````````````````````````````````

Il existe souvent deux limites sur le nombre maximum d'enregistrements retournés par une requête LDAP :

* la limite du client (définie par exemple sur Debian/Ubuntu dans ``/etc/ldap/ldap.conf``)
* la limite imposée par le serveur : si la limite définie par le client est supérieure à la limite serveur, c'est cette dernière qui prend le dessus.

.. warning::

   Si la limite est atteinte l'option de comportement lors de la suppression d'un utilisateur de l'annuaire ne peut fonctionner. De plus, GLPI affichera un message d'avertissement lors d'un import ou d'une synchronisation.

Avec PHP 5.4 ou supérieur, il est désormais possible de contourner la limitation du sizelimit en activant, dans l'onglet *Informations avancées*, la **pagination des résultats**. Dans ce mode, PHP va requêter l'annuaire autant de fois que nécessaire et par tranche de X résultats jusqu'à ce que l'ensemble des enregistrements soient renvoyés.

L'option **Taille des pages** permet d'ajuster cette valeur de même que **nombre maximum de résultats** définit la limite d'enregistrement à ne pas dépasser lors d'une requête LDAP (afin par exemple d'éviter une erreur indiquant que PHP demande plus de mémoire que ce qui lui est alloué).

.. note::

   Sur un annuaire OpenLDAP la limite par défaut est à 500 enregistrements, sur un Active Directory elle est de 1000.

   Sur un Active directory il est possible de modifier la valeur du `MaxPageSize` grâce aux commandes suivantes (attention cette modification est globale à tout l'annuaire) :

   .. code-block::

      C:> ntdsutil
      ntdsutil: ldap policies
      ldap policy: connections
        server connections: connect to server 192.168.1.1 ( here a few messages regarding connectivity are displayed)
      server connections : q
      ldap policy : show values ( here we will see all the values including MaxPageSize which is 1000 currently)
      ldap policy : set maxpagesize to 5000
      ldap policy : commit changes
      ldap policy : q
      ntdsutil : q

Replicates
~~~~~~~~~~

If a LDAP directory is not accessible, users will no longer be able to connect to GLPI. In order to avoid this situation, replicates can be declared: they share the same configuration as the server they are replicating, but are available at a different address.

Replicates are used only in the event of a loss of connection to the master directory. Replicates are added on the directory form, by entering a **name** which will be displayed in GLPI, as well as a **host name** and a **port**. There is no limit to the number of directories replicated.

.. include:: ../../tabs/historical.rst

.. include:: ../../tabs/all.rst

The different actions
---------------------

LDAP directories do not have specific actions, refer to :doc:`common actions</modules/overview/actions>`.

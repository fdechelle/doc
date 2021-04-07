LDAP Directories
================

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

    Note that this filter is automatically added when the Active Directory pre-configuration model is selected.

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

For Active Directory, if the ``userprincipalname`` is used instead of the ``samaccountname``, the ``rootdn`` can be under the form ``prenom.nom@domaine.fr``.

Parameters to be entered are simple, as in:

* host: ``ldap.mycompany.fr``
* basedn: ``dc=mycompany,dc=fr``

This should be enough if anonymous search is allowed. Otherwise, and if all the users are not positioned within the same DN, you must specify the DN of an authorized user and his password: rootdn/Pass. For Active Directory, it is mandatory to enter an account that has the right to authenticate on the domain.

By attempting to connect to the directory using an LDAP browser, it is possible to test these parameters. There are many LDAP browser, but the following can be mentioned:

* *LdapBrowser Editor*: free software written in Java and therefore multi-platform
* *ADSIedit* for Active Directory: this tool can be found in support tools of the Windows Server installation CD.

.. note::

   If some of the users have connection restrictions to certain machines configured in their AD profile, the following error is possible when trying to login on the GLPI home page: **User not found or several identical users found**. The solution is to add the server hosting the AD to the list of machines the user can connect to.

Test
~~~~

Allows to test the configuration defined in the LDAP Directory tab.

The message **Connection test succeeded** indicates that GLPI was able to connect to the LDAP directory with the information provided (host, port, user account).

Next task is users import. Before performing it, the other parameters (connection filter, login field...) must be carefully checked.

Users
~~~~~

Allows to configure how the link will be made between the fields of the directory and those of GLPI. For each GLPI field (name, first name, picture, etc.) a field from the directory is associated.

.. figure:: /modules/configuration/images/ldap-users.png
   :alt: Users LDAP configuration
   :align: center
   :scale: 50%

   Users LDAP configuration

Groups
~~~~~~

Allows to configure the group storage method at the directory level.

.. image:: /modules/configuration/images/ldap-groups.png
   :alt: Groups LDAP Configuration
   :align: center
   :scale: 50%

   Groups LDAP Configuration

Advanced information
~~~~~~~~~~~~~~~~~~~~

.. figure:: /modules/configuration/images/ldap-users.png
   :alt: Users LDAP configuration
   :align: center
   :scale: 50%

   Users LDAP configuration

If the time of the machine hosting the LDAP directory is not in the same time zone as the machine hosting GLPI, the **Time zone** variable must be modified in order to adjust the delay: otherwise, this can cause erroneous results in the list of users to synchronize.

Secure LDAP connection
``````````````````````

GLPI manages secure connection to an LDAP directory through an SSL connection, also called LDAPS. It is enough to add in front of the host name or its IP ``ldaps://`` as well as changing the port (default 636). For example, local LDAPS access will be: 

* Host: ``ldaps://127.0.0.1`` 
* Port: ``636``

Limit on the number of returned records (sizelimit)
```````````````````````````````````````````````````

There are often two limits on the maximum number of records returned by an LDAP query:

* the client limit, defined for example on Debian/Ubuntu in ``/etc/ldap/ldap.conf``
* the limit imposed by the server: if the limit defined by the client is greater than the server limit, the latter takes precedence

.. warning::

   If the limit is reached the behavior option when deleting a user from the directory may not work. In addition, GLPI will display a warning message during an import or a synchronization.

With PHP 5.4 or higher, it is now possible to bypass the sizelimit limitation by activating, in the *Advanced information* tab, the **pagination of results**. In this mode, PHP will query the directory as many times as necessary and in slices of X results until all the records are returned.

The option **Size of pages** is used to adjust this value as well as **maximum number of results** which defines the records limit not to be exceeded during an LDAP request, in order for example to avoid an error indicating that PHP is asking for more memory than what is allocated to it.

.. note::

   On an OpenLDAP directory the default limit is 500 records, on an Active Directory it is 1000.

   On an Active directory it is possible to modify the value of the ``MaxPageSize`` using the following commands (beware that this modification is global to the entire directory):

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

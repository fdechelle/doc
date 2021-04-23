Configure controls
==================

GLPI has a mechanism for performing checks before inserting an object into the database.

This functionality makes it impossible to add or update an item if another item already has an identical value. This mechanism applies to manual additions as well as importing from an external source such as from an inventory tool.


The different tabs
------------------

Field unicity
~~~~~~~~~~~~~

Uniqueness is defined by a name, a type of object to which it relates, a list of fields as well as the resulting actions (refusal of database injection, sending of notification). The sub-entity field is used to indicate whether the uniqueness criteria apply to all GLPI or only to the entity in which the uniqueness is created.

.. note:: the selection of several fields verifies the uniqueness of the tuple and not each field individually.

For a computer, the overall uniqueness criterion is the serial number. If an attempt is made to register, regardless of the entity another having the same serial number, the insertion is refused and an error message indicates the element already present in the database. However, if a user inserts a computer without a serial number, then no uniqueness check will be performed.

Criteria added to blacklists will be ignored when calculating uniqueness, see :doc:`Configure dropdown</modules/configuration/dropdown/general>`.

Duplicate
~~~~~~~~~

This tab lists all the values ​​corresponding to the criteria which are currently duplicated in the GLPI database, possibly with a link for each of them to the item form.

Historical
~~~~~~~~~~

See :doc:`Tab "Historical" </modules/tabs/historical>`

.. include:: ../tabs/debug.rst

.. include:: ../tabs/all.rst


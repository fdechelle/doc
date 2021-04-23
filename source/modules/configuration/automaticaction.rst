Configure automatic actions
===========================

The automatic action **watcher** is an action that monitors the correct execution of other automatic actions. If an automatic action is in error, a notification will be sent. Email monitoring must therefore be activated, see :doc:`Configure notifications </modules/configuration/notification/notificationconfiguration>`; the recipients can be configured in the **Crontask Watcher** notification, see :doc:`Manage notifications by entity </modules/configuration/notification/notification>`.

The different tabs
------------------

* **Automatic action**:

  For each action, the following fields can be configured:

  * **Frequency of execution**

  * **Status** : allows if necessary to deactivate the action

  * **Execution mode**:

    * ``GLPI``: triggered by users browsing (this is set by default in standard installation)
    * ``CLI``: more robust and steady but requires a system configuration

  * **Execution time range**: allows to deactivate some processing, at night for example

  * **Time in days to keep logs**:  how long to keep automatic action logs stored in the database

  The interface also allows to reset the execution date and manually force the execution.

  Some automatic actions can have specific parameters, such as the maximum number of emails to send each time for the ``mailqueue`` action. Likewise, plugins can define their own automatic actions.

* **Statistics**: displays information about the execution of this task (number of executions, start date, minimum, maximum, average and total durations)

* **Logs**: lists the last executions according to the parameter defined in the *Automatic action* tab (see above). A link on the execution date allows to see the details of a specific execution.

The different actions
---------------------

* **Disable an automatic action**: change status to ``Disabled``
* **Unlock an automatic action**: in some cases, an automatic action may be blocked, for instance shutdown of the database for backup when the automatic action controlling the replicates is active. In this case, clicking on the cross to the right of the word ``running`` will unblock it

.. todo:: check link
    * | **:doc:`Lancer les actions automatiques en ligne de commande <../glpi/config_crontaskcli.html>`** | L'ordonnanceur des tâches de GLPI peut-être appelé de manière externe, depuis la ligne de commande, en exécutant le fichier front/cron.php.


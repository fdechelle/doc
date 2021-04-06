Escalation levels
=================

Des niveaux d'escalades peuvent être définis au sein d'un SLA. Chaque niveau déclenche des actions automatiques permettant la résolution du ticket dans les meilleurs délais. Un niveau se déclenche avant ou après la date d'échéance du SLA en fonction du délai défini.

.. topic:: Example: level change

   Par exemple, un jour avant l'échéance, le ticket est affecté au support de niveau 2 et sa priorité passée à Haute.

Les niveaux d'escalades peuvent être conditionnés par des critères de déclenchement. Sans critère, le niveau sera déclenché mais si des critères sont définis, ils seront contrôlés avant application du niveau d'escalade.

.. topic:: Example: trigger

   Par exemple, si 1 jour avant la date d'échéance vous souhaitez envoyer un rappel à l'administrateur si le ticket est toujours à l'état *Nouveau*, il faut définir comme critère `Status est Nouveau`.

The different tabs
------------------

* **Onglet "Critères"**: Permet d'ajouter un nouveau critère et liste les critères déjà définis pour ce niveau d'escalade.

* **Onglet "Actions"**: Permet d'ajouter une action qui sera exécutée si le critère défini est rempli. Il liste également les actions déjà définies pour ce niveau d'escalade.

* :doc:`Onglet "Historique" </modules/tabs/historical>`: l'historique est visualisé depuis l'onglet *Historique*

.. include:: ../../tabs/debug.rst

.. include:: ../../tabs/all.rst

The different actions
---------------------

* **Add a new escalation level**: this action is done in tab *Escalation levels* of a SLA


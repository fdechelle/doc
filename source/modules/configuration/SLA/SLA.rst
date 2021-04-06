Configurer les SLAs
===================

.. |NiveauSla| image:: /modules/configuration/images/NiveauSla.png

.. toctree::
   :maxdepth: 1

   escalationlevel

Un SLA (Service Level Agreement ou accord de niveau de service) est la formalisation d'un contrat négocié entre le ServiceDesk et le client définissant le niveau de service attendu et donc au délai maximum pour résoudre un incident ou une demande (J+1, H+4...).

Les SLAs sont associables aux tickets via le moteur de règles des tickets (voir :doc:`Règles métier pour les tickets <07_Module_Administration/05_Règles/04_Règles_métier_pour_les_tickets.rst>`).  L'association du SLA au ticket permet le calcul automatique de sa date d'échéance. Plusieurs SLAs peuvent ainsi être définis et affectés suivant des critères précis.

.. topic:: Example: SLA

   Par exemple, le SLA 1 sera affecté si le ticket est associé à une catégorie spécifique et le SLA 2 pour les autres catégories.

.. warning::
   * Si un SLA est affecté manuellement à l'ouverture du ticket (par l'utilisateur ou via un gabarit de ticket), les règles métiers ne pourront pas redéfinir celui-ci. 
   * Un SLA peut être affectée a posteriori. A l'affectation de celui-ci, il sera complètement rejoué et les actions associées aux niveaux d'escalade passés seront exécutées.

Un calendrier peut être associé à un SLA (voir :doc:`Configurer les intitulés </modules/configuration/02_Intitulés/01_Intitulés.rst>`).  Par défaut, aucun calendrier n'est associé et les calculs se font sur une base de travail 7 jours sur 7 et 24 heures sur 24. Il est également possible d'utiliser le calendrier associé au ticket (i.e. celui de l'entité à laquelle est rattaché le ticket).

.. note:: Si le temps maximum de résolution est exprimé en jours, l'ensemble des calculs se feront en jours (J+1, J+4 par exemple) en tenant compte du calendrier pour déterminer les jours ouvrés. Dans le cas de l'utilisation du témoin Fin de la journée de travail, la date d'échéance correspondra à la fin du jour ouvré correspondant.  Si le temps maximum de résolution est exprimé en heures ou en minutes alors les calculs seront réalisés en tenant compte des horaires d'ouvertures.

.. topic:: Example: calendar

   Par exemple pour un SLA en H+4 avec un calendrier définissant des horaires d'ouverture de 8h à 18h, un ticket ouvert à 16h aura une date d'échéance le lendemain à 10h.

Le passage du ticket au statut en attente met le SLA en sommeil. Si le ticket reste en attente 3 heures par exemple, la date d'échéance sera repoussée de 3 heures.

The different tabs
----------------------

* **:doc:`Onglet "Niveaux d'escalade" </modules/configuration/SLA/escalationlevel>`** Permet d'ajouter un nouveau niveau d'escalade à ce SLA et liste des différents niveaux déjà définis avec pour chaucun leurs critères et leurs actions. |NiveauSla| Pour modifier un niveau il suffit de cliquer sur son nom.

* **Onglet "Règles"** Liste les règles métier liées à ce SLA.

.. include:: ../../tabs/tickets.rst

Pour les SLA, il n'est pas possible d'ajouter un ticket. L'onglet liste juste les tickets affectés à ce SLA.

* :doc:`Onglet "Tous" <Les_différents_onglets/Onglet_Tous.rst>`: pour un élément, toutes les informations sont affichées sur une seule page.

The different actions
-----------------------

* :doc:`Add a SLA <Les_différentes_actions/Créer_un_nouvel_objet.rst>`
* :doc:`Display a SLA <Les_différentes_actions/Visualiser_un_objet.rst>`
* :doc:`Modify a SLA <Les_différentes_actions/Modifier_un_objet.rst>`
* :doc:`Delete a SLA <Les_différentes_actions/Supprimer_un_objet.rst>`
* **Add a new escalation level**: this action is done in tab *Escalation levels*


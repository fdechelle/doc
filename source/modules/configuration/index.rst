Configuration
=============

Le module Configuration permet d'accéder aux options de configuration générale de GLPI : la configuration globale de GLPI, les notifications, les collecteurs, les tâches automatiques, l'authentification, les plugins, les critères d'unicité et les liens externes protocolés.

Les intitulés ne proposent pas d'actions spécifiques, se reporter aux :doc:`actions communes <../generalites/actions>`.

.. note::

   Si des éléments que vous voulez supprimer sont utilisés, GLPI proposera automatiquement de transférer les entrées existantes vers un autre élément de la liste, ou bien de les remettre à zéro.

-   **[Configurer les composants](/modules/configuration/03_Composants.rst)**
     
-   **[Configurer les notifications](/modules/configuration/notification/notificationconfiguration)**
     Configurer les suivis par courriels, créer des modèles de notifications, définir l'envoi de notification.

-   **[Configurer les SLAs](/modules/configuration/SLA/SLA)**
     Définir les SLA ainsi que les différents niveaux d'escalade.

-   **[Configurer les paramètres centraux](/modules/configuration/general/centralparameter)**

-   **[Configurer les contrôles](/modules/configuration/07_Controles.rst)**
     
-   **[Configurer les actions automatiques](/modules/configuration/automaticaction)**
     
-   **[Configurer les collecteurs](../glpi/config_mailcollector.html)**\
    La configuration des collecteurs s'effectue depuis le menu
    Configuration \> Collecteurs
-   **[Ajouter un
    collecteur](../glpi/config_mailcollector_t_create.html)**\
-   **[Supprimer un
    collecteur](../glpi/config_mailcollector_t_delete.html)**\
-   **[Configurer les liens externes
    protocolés](../glpi/config_link.html)**\
    Les liens externes se configurent depuis le menu Configuration \>
    Liens externes
-   **[Ajouter un lien externe](../glpi/config_link_t_create.html)**\
-   **[Supprimer un lien externe](../glpi/config_link_t_delete.html)**\
-   **[Configurer les plugins GLPI](../glpi/config_plugin.html)**\
    Les plugins dans GLPI, installation, configuration, activation

.. toctree::
   :maxdepth: 2

   authentication/index
   dropdown/index
   SLA/SLA
   automaticaction
   component
   control
   external_link
   notification/notification
   general/index

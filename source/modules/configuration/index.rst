Configuration
=============

The Configuration module provides access to the general configuration options of GLPI: global configuration of GLPI, notifications, collectors, automatic tasks, authentication, plugins, uniqueness criteria and protocoled external links.

.. Why here? Les intitulés ne proposent pas d'actions spécifiques, se reporter aux :doc:`actions communes <../generalites/actions>`.

.. note::

   If elements to be deleted are used, GLPI will automatically propose to transfer the existing entries to another element in the list, or to reset them.

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


Big mess:

* **[Configurer les collecteurs](../glpi/config_mailcollector.html)**\
    La configuration des collecteurs s'effectue depuis le menu Configuration \> Collecteurs
* **[Add a collecteur](../glpi/config_mailcollector_t_create.html)**\
* **[Delete a collecteur](../glpi/config_mailcollector_t_delete.html)**\
* **[Configurer les liens externes protocolés](../glpi/config_link.html)**\
    Les liens externes se configurent depuis le menu Configuration \> Liens externes
* **[Add a lien externe](../glpi/config_link_t_create.html)**\
* **[Delete a lien externe](../glpi/config_link_t_delete.html)**\
* **[Configurer les plugins GLPI](../glpi/config_plugin.html)**\
    Les plugins dans GLPI, installation, configuration, activation

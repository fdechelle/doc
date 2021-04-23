Configure components
====================

The components added to the computers can be configured.

A hardware component is defined by a type, a name, a manufacturer, a comment as well as several fields specific to the type of the component. For example, for a motherboard, chipset can be entered there.

The list of the different types of component is fixed:

.. figure:: images/component_dropdown.png
   :alt: List of component types
   :align: center

   List of component types
	   
.. note:: It is possible to enter other types of components inside the *Other components* type. However, it is not possible to add other types than those listed here.

Once a component type has been selected (*Motherboard*, *Processor* ...), the list of already registered components is automatically accessed.

.. figure:: images/component_list.png
   :alt: List of components
   :align: center

   List of components

The different tabs
------------------

Main
~~~~

Information that defines a hardware component, depending on the type of component.

.. figure:: images/component_details.png
   :alt: Detail of a processor type component
   :align: center

   Detail of a processor type component


Elements
~~~~~~~~

This tab allows to display computers linked to the component. 

The following information will be displayed:

* Computer name
* Frequency for this computer
* Number of cores for this computer
* Number of threads for this computer

.. figure:: images/component_elements.png
   :alt: Element of a component
   :align: center

   Element of a component

.. note::
   It is possible to modify the characteristics of a component only for the linked element.

   From the *Elements* tab of the component, click on the **Update** link. Several tabs are then proposed:

   * "Element - Component name link" tab: list the characteristics of this component
   * :doc:`Tab "Management" </modules/tabs/management>`: manage financial and administrative information
   * :doc:`Tab "Documents" </modules/tabs/documents>`
   * :doc:`Tab "Historical" </modules/tabs/historical>`
   * :doc:`Tab "Debug" </modules/tabs/debug>`: only if you are connected in *Debug* mode
   * :doc:`Tab "All" </modules/tabs/all>`: for an element, all information is displayed on one page

.. include:: ../tabs/documents.rst

.. include:: ../tabs/historical.rst

.. include:: ../tabs/all.rst

Configure protocoled external links
===================================

External links are configured from the *Configuration> External links* menu.

Some items of GLPI can be associated with a set of links to external applications. These are visible from the *Links* tab of the different forms.

To configure a link, it is possible to use specific tags which will be replaced by the values ​​of the item. Valid tags are:

* ``[LOGIN]``: user ID
* ``[ID]``: internal numeric identifier of the object
* ``[NAME]``: object name
* ``[LOCATION]``: object location
* ``[LOCATIONID]``: internal identifier of the location
* ``[IP]``: object's IP address
* ``[MAC]``: MAC address of the object
* ``[NETWORK]``: network in which the object is located
* ``[DOMAIN]``: object network domain
* ``[SERIAL]``: serial number
* ``[OTHERSERIAL]``: inventory number
* ``[USER]``: user associated with the hardware
* ``[GROUP]``: group associated with the material
* ``[FIRSTNAME]``: user's first name (only for users)
* ``[REALNAME]``: username (only for users)

Each link can be associated with one or more types of items.

If the content is empty, a simple link will be generated. If any content is present, a link to content download will be generated.

Link may be opened in a new window depending on the *Open in a new window* setting.

Web type link
-------------

To create a web type link, create a protocoled external link having as name: ``http://[IP]``; assign it to network equipment.

RDP type link
-------------

For remote access to computers, create an external protocol link with the name ``Remote access.rdp'' and configure the **File content** by inserting the content of an RDP type file and replacing ip/name/domain by tags ``[IP]``, ``[NAME]``, ``[DOMAIN]``.

.. note:: when using tags coming from network ports (``IP``, ``MAC``), if the equipment has more than one, then this will create as many links as there are ports. For example for a machine with 2 different IP addresses, 2 links will be displayed.

Remote control through the VNC applet
-------------------------------------

Some VNC implementations provide an applet that allows you to control a computer through a browser. Usually, the port used is 5900. The corresponding link will be of the type ``http://[IP]:5900`` or ``http://[NAME].[DOMAIN]:5900``.

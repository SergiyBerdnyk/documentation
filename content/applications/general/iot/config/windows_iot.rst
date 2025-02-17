========================
Connect Windows IoT Odoo
========================

A Virtual IoT box is a computer program that needs to be downloaded and installed on a Windows
computer. This requires a Windows operating system with an Odoo 16 or later database.

The Windows virtual :abbr:`IoT (Internet of Things)` box works the same way as a physical :abbr:`IoT
(Internet of Things)` box, with the ability to run most of the same devices. All :abbr:`POS (Point
of Sale)` devices work with it, such as a scale or printer. Payment terminals will also work, but it
should be noted that :abbr:`MRP (Material Requirement Planning)` devices are not compatible. *These
include cameras or measurement tools.*

Pre-requisites
==============

The following items will be needed to complete the Windows :abbr:`IoT (Internet of Things)`
installation.

- Odoo 16 database or any version above.
- :abbr:`IoT (Internet of Things)` compatible devices (except those mentioned above). Refer to:
  `Odoo's compatible IoT devices <https://www.odoo.com/app/iot-hardware>`_.
- Device drivers for Windows.

  .. note::
     Odoo recommends using an updated, recent version of Windows (Windows 10/11) as some older
     operating systems can cause the Windows virtual :abbr:`IoT (Internet of Things)` to not work.

- Windows computer (laptop, desktop, or server).
- Odoo :abbr:`IoT (Internet of Things)` subscription. Refer to: :ref:`iot/iot-eligibility`.

Connect the Windows virtual IoT box to an Odoo database
=======================================================

The Windows virtual IoT box is simple to setup in just a few easy steps. Follow this process when
installing the Windows virtual IoT software for the first time.

Download and initial installation
---------------------------------

To begin the installation, navigate to the Odoo 16 or higher installation package for Enterprise or
Community - Windows edition at `Odoo's download page <https://odoo.com/download>`_. Next, install
and setup the Odoo :file:`.exe` file. After the instructions screen, click :guilabel:`Next` to start
the installation and agree to the :abbr:`TOS (Terms of Service)`.

During the next step of the installation, select :guilabel:`Odoo IoT` from the :guilabel:`Select the
type of install` drop-down menu.

.. example::
   For reference, the following should be installed:

   - **Odoo server**
   - **Odoo IoT**
   - **Nginx WebServer**
   - **Ghostscript interpreter**

Ensure there is enough space on the computer for the installation and click :guilabel:`Next`.

Setting the destination and completing the installation
-------------------------------------------------------

To complete the installation, select the :guilabel:`Destination Folder` and click
:guilabel:`Install`.

.. tip::
   Choosing ``C:\odoo`` as the install location will allow for the Nginx server to start. If the
   folder doesn't exist, then create it. Otherwise the installation files will be spread throughout
   the hard drive.

.. warning::
   Odoo's Windows virtual IoT software should not be installed inside any of the Window's User's
   directories. Doing so will not allow for Nginx to initialize.

The installation may take a few minutes. When complete, click :guilabel:`Next` to continue.

Ensure that the :guilabel:`Start Odoo` box is checked and click :guilabel:`Finish`. After
installation, the Odoo server will run and automatically open `http://localhost:8069` on a web
browser. The webpage should display the :abbr:`IoT (Internet of Things)` box homepage.

.. seealso::
   A restart of the Windows IoT program may be necessary should the web browser not display
   anything. :ref:`iot/restart_windows_iot`

Connecting devices
------------------

Next, connect the :abbr:`IoT (Internet of Things)` devices to the Windows computer. Windows should
automatically detect the device because the driver is pre-installed on the computer. If not, search
for and install the Windows driver for the device.

.. important::
   Most devices connect to the Windows Machine for Windows IoT automatically through Windows
   Plug-N-Play (PnP). However, if Windows does not automatically recognize the device after
   connecting, then the administrator may need to install the corresponding drivers manually.

   Devices automatically recognized:

   - Regular ink/toner based printers
   - Receipt printers (Epson/Star)
   - Barcode scanners
   - Measurement devices (although some configuration of the measurement device settings is
     required) See this documentation: :doc:`../devices/measurement_tool`

   Devices not automatically recognized (requires manual driver download):

   - Label printers (Zebra)
   - Scales

   Reference the manufacturer's website for the equipment in question. Then, download the drivers
   and install them on the Windows machine. Reconnect the device in question and Windows will find
   the device.

Following connecting devices to the computer, refresh the :abbr:`IoT (Internet of Things)` box
homepage and verify the device is seen. If not, reload the handlers through the :abbr:`IoT (Internet
of Things)` box homepage.

Finally, connect Windows :abbr:`IoT (Internet of Things)` to a database using existing instructions
(manually using the Token).

.. seealso::
   :doc:`/applications/general/iot/config/connect`

Now the installation is complete, the devices connected to :abbr:`IoT (Internet of Things)` can be
used to complete processes/actions.

Troubleshooting
===============

.. _iot/restart_windows_iot:

Restart Windows IoT box
-----------------------

In some instances a manual restart of the physical :abbr:`IoT (Internet of Things)` box can resolve
the issue of an :abbr:`IoT (Internet of Things)` box not showing up on the database. For the Windows
virtual :abbr:`IoT (Internet of Things)` box a manual restart of the Odoo server can resolve
database connection issues.

To restart the virtual Windows IoT server:

#. Type `Services` into the Windows :guilabel:`Search Bar`.
#. Select the :menuselection:`Services` App and scroll down to the :guilabel:`Odoo` service.
#. Right click on :guilabel:`Odoo` and select :guilabel:`Start` or :guilabel:`Restart`. This action
   will manually restart the Odoo IoT server.

Firewalls
---------

Firewalls keep devices safe and secure. Sometimes they can block connections that should be made
though. The Windows virtual :abbr:`IoT (Internet of Things)` box software may not be reachable to
the :abbr:`LAN (Local Area Network)` due to a firewall preventing the connection. Consult your local
IT support team to make exceptions (network discovery) in the :abbr:`OS (Operating System)` or
firewall program. Windows has their own firewall as do other virus protection programs.

.. example::
   A client might encounter a time when they are able to reach the homepage of the :abbr:`IoT
   (Internet of Things)` box, yet they cannot access it from another computer/mobile device/tablet
   on the same network.

Making an exception on Windows Defender
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible to allow other devices to access the Windows virtual :abbr:`IoT (Internet of Things)`
box while keeping the firewall on. This is done by creating a rule on *Windows Defender* and
allowing communication through port `8069`. The following process describes the steps to take in
order to make this exception.

Create a rule in Windows Defender
*********************************

First, open the *Windows Firewall* by navigating to the :menuselection:`Start Menu` and typing in
`Firewall`. Then, open the :menuselection:`Windows Defender Firewall` program. In the left-hand
menu, navigate to :guilabel:`Advanced Settings`.

Once :guilabel:`Advanced Settings` have been selected, click :guilabel:`Inbound Rules` in the
left-hand menu. Then, in the right-hand menu column (under :guilabel:`Inbound Rules`), click on
:guilabel:`New Rule` to create a new rule.

Configure new rule
******************

On the :menuselection:`Rule Type` screen, select :guilabel:`Port`. Then click :guilabel:`Next`. From
the :menuselection:`Protocol and Ports` page leave the rule application to :guilabel:`TCP`. Then,
select :guilabel:`Specific Local Ports` for the :guilabel:`ports` option. In the text box, type in
`8069, 443`. Finally, click :guilabel:`Next` to continue to the next step.

On the :menuselection:`Actions` page, select :guilabel:`Allow the connection` and click
:guilabel:`Next`. The following page on the :menuselection:`Rule Configuration` wizard is the
:guilabel:`Profile` page. On this page, select whichever connection type applies to the network the
Windows machine is operating on. Ideally, select :guilabel:`Private` only connections. The *Private*
connection type is the most secure connection while allowing the selected port to communicate. Click
:guilabel:`Next` to continue.

Finally, assign a new, unique name to the rule. For example, this name can be `Odoo`. Optionally,
add a brief description in the :guilabel:`Description` field. Click :guilabel:`Finish` to complete
the :guilabel:`Rule Configuration` wizard. Now, the new rule is active and devices can connect to
the Windows virtual :abbr:`IoT (Internet of Things)` box.

Worldline exception
~~~~~~~~~~~~~~~~~~~

*Worldline* is a payment terminal that can be connected to Odoo's *PoS* (point of sale) system. It
allows for a comprehensive and fluid payment experience for customers. Worldline is available in
Benelux (coalition of Belgium, the Netherlands, and Luxembourg).

When using the Windows IoT server to connect the Worldline payment terminal, it is necessary to
create an exception in the Windows firewall so that a connection can be made between the Odoo
database/:abbr:`IoT (Internet of Things)` box and Worldline.

.. seealso::
   :doc:`../../../sales/point_of_sale/payment_methods/terminals/worldline`

To create the exception, first, open the *Windows Defender Firewall* app on the Windows machine.
This can be accomplished by typing `windows defender` in the :guilabel:`Search` bar.

Next, click :guilabel:`Advanced settings` in the left menu.

.. image:: windows_iot/advanced-settings.png
   :align: center
   :alt: Advanced settings option highlighted in the left pane of the Windows Defender Firewall app.

In the left menu, choose :guilabel:`Inbound Rules`.

.. image:: windows_iot/inbound-rules.png
   :align: center
   :alt: Windows Defender left window pane with inbound rules menu item highlighted.

After selecting :guilabel:`Inbound Rules`, select :guilabel:`New Rule` in the far right menu.

.. image:: windows_iot/new-rule.png
   :align: center
   :alt: New rule dropdown shown with new rule option highlighted.

Then, for the :guilabel:`Rule Type`, select the radio button for :guilabel:`Port`. Click
:guilabel:`Next` to continue to the rest of the configuration.

.. image:: windows_iot/radio-port.png
   :align: center
   :alt: Rule Type window open, with the radio button next to port highlighted.

On the :guilabel:`Protocols and Ports` page, choose the radio button for :guilabel:`TCP`, under
:guilabel:`Does this rule apply to TCP or UDP?`.

Next, under :guilabel:`Does this rule apply to all local ports or specific ports?`, select the radio
button for :guilabel:`Specific local ports`. Then, enter `9050`, and click :guilabel:`Next` to
continue.

.. image:: windows_iot/protocol-port.png
   :align: center
   :alt: Protocol/port configuration window with TCP, specific port (9050) and Next highlighted.

The next screen is the :guilabel:`Action` page. Under :guilabel:`What action should be taken when a
connection matches the specified conditions?`, choose the radio button for :guilabel:`Allow the
connection`. Then, click :guilabel:`Next` to continue.

A :guilabel:`Profile` page appears. Under :guilabel:`When does this rule apply?`, leave the three
boxes checked for: :guilabel:`Domain`, :guilabel:`Private`, and :guilabel:`Public`. Click
:guilabel:`Next` to continue to the naming convention page.

On the :guilabel:`Name` page, enter `Odoo Worldline`, under the :guilabel:`Name` field. Enter a
:guilabel:`Description (optional)`. Finally, once ready, click :guilabel:`Finish`.

The final :guilabel:`Inbound rule` should appear as follows:

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - Odoo Worldline
   * - Profile
     - All
   * - Enabled
     - Yes
   * - Action
     - Allow
   * - Override
     - No
   * - Program
     - Any
   * - Local Address
     - Any
   * - Remote Address
     - Any
   * - Protocol
     - TCP
   * - Local Port
     - 9050
   * - Remote Port
     - Any
   * - Authorized Users
     - Any
   * - Authorized Computers
     - Any
   * - Authorized Local Principals
     - Any
   * - Local User Owner
     - Any
   * - PolicyAppld
     - None
   * - Application Package
     - Any

Uninstalling Windows IoT
------------------------

Uninstalling the Windows virtual :abbr:`IoT (Internet of Things)` box is done through the Windows
program manager. Using any Windows version, search for `program`. Then, select :guilabel:`Add or
Remove Programs` located in the control panel. Search for `Odoo` and click the :guilabel:`three dot
menu` to uninstall.

Confirm the un-installation and follow the steps to uninstall through the Odoo uninstall guide.

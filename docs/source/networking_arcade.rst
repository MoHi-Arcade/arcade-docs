Arcade Networking Overview
==========================

Architecture
------------

The arcade network is built around a MikroTik access point/router.

- The MikroTik operates in **station mode**, connecting to the school WiFi.
- It functions as a **NAT router**, creating a private internal network.
- The Raspberry Pi (RetroPie) and internal devices connect via Ethernet to the MikroTik.
- External Ethernet ports in the access hatch feed into the MikroTik.

Flow:

    School WiFi → MikroTik (station + NAT) → Internal Ethernet → Raspberry Pi

Fallback Access
---------------

If wireless connectivity fails:

1. Open the access hatch.
2. Plug a laptop into one of the exposed Ethernet ports.
3. This connects directly into the MikroTik’s internal network.

MikroTik Configuration (WinBox)
-------------------------------

Connection Steps
^^^^^^^^^^^^^^^^

1. Connect laptop via Ethernet to the arcade.
2. Open WinBox on the laptop.
3. Navigate to the **Neighbors** tab.
4. Identify the MikroTik device (by MAC address or name).
5. Click the device entry.
6. Enter credentials (see Google Doc).
7. Connect.

Notes:
- MAC-based connection is preferred if IP is unknown.
- Device IP information is stored in the password document.

What the MikroTik Is Doing
^^^^^^^^^^^^^^^^^^^^^^^^^^

- Connecting to school WiFi as a client.
- Performing NAT for internal devices.
- Providing a stable wired network to the Raspberry Pi.

Users are not expected to deeply reconfigure the MikroTik.
If issues occur beyond basic reconnection, use external documentation.

Basic Troubleshooting
---------------------

No Internet on Arcade
^^^^^^^^^^^^^^^^^^^^^

- Check if MikroTik is connected to WiFi in WinBox.
- Verify signal strength and SSID.
- Reconnect to the correct network if needed.

Cannot Connect via WinBox
^^^^^^^^^^^^^^^^^^^^^^^^^

- Ensure Ethernet is plugged into access hatch.
- Use MAC-based connection instead of IP.
- Confirm laptop is set to DHCP.

Security Notes
--------------

- Do not expose the MikroTik directly to external networks.
- Credentials are stored in the Google Doc.
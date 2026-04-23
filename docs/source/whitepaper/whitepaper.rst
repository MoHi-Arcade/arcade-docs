Arcade System White Paper
========================

Overview
--------

This document provides a complete technical overview of the arcade system, including hardware architecture, software stack, networking, input systems, and deprecated subsystems.

The system is designed as a self-contained arcade cabinet powered by a Raspberry Pi running RetroPie, with modular input hardware and remote management capabilities.

Primary goals:
- Reliable arcade gameplay
- Minimal user-facing complexity (kiosk mode)
- Maintainability via internal access and remote tools
- Expandability for future features

System Architecture
-------------------

Core Components
^^^^^^^^^^^^^^^

- Raspberry Pi (RetroPie host)
- USB input encoders (buttons + joysticks)
- USB trackball
- MikroTik router (network bridge + NAT)
- Display + lighting system (timer-controlled)
- Internal power distribution (5V + AC separation)

High-Level Flow
^^^^^^^^^^^^^^^

::

   User Input → USB Encoders → Raspberry Pi (RetroPie + RetroArch)
              → Video Output → Display

   Network:
   School WiFi → MikroTik (station mode + NAT) → Ethernet → Raspberry Pi

Physical Design
---------------

Access Hatch
^^^^^^^^^^^^

The access hatch exposes critical infrastructure:

- Mechanical timer (display + lighting)
- USB hub (connected to Raspberry Pi)
- Ethernet ports (internal network access)

The timer:
- Uses a rotating dial for current time
- Uses physical pins for scheduling
- Includes an override switch for always-on mode

Always-on mode should only be used temporarily due to:
- Burn-in risk
- Fire risk
- Component wear

Button Panel and Internal Hardware
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The button panel is removable via spring-loaded pins.

Internal components include:

- Raspberry Pi (mounted with unsecured bolts)
- USB encoders (input handling)
- Power busbars (lighting distribution)
- Anderson Powerpole connectors (modular wiring)

Button wiring is split into two systems:

1. Input (switch contacts inside grey housing)
2. Lighting (side terminals with polarity)

All control electronics are low voltage (5V), but AC power exists elsewhere in the cabinet and should not be touched.

Software Stack
--------------

RetroPie and RetroArch
^^^^^^^^^^^^^^^^^^^^^^

The system runs RetroPie on a Raspberry Pi.

Responsibilities:
- EmulationStation: frontend UI
- RetroArch: emulator backend
- Linux OS: system-level control

Characteristics:
- Linux-based, fully accessible via CLI
- Prone to SD card corruption if improperly powered off
- Backups are maintained as disk images

Game Management
^^^^^^^^^^^^^^^

Games are stored under:

::

   /home/pi/RetroPie/roms/<system>/

Supported management methods:
- SFTP
- CLI (scp, mv, rm)

Game metadata is managed via EmulationStation gamelist XML files.

Due to complexity and fragility, game management is restricted and should be approached cautiously.

Input System
------------

USB Encoders
^^^^^^^^^^^^

- Translate button presses into input signals
- Appear as standard HID devices

RetroArch Input Layers
^^^^^^^^^^^^^^^^^^^^^^

1. RetroPie-level configuration (global device mapping)
2. RetroArch global bindings
3. Core-specific overrides
4. Per-game overrides

Overrides take precedence in that order.

Trackball Integration
^^^^^^^^^^^^^^^^^^^^^

The trackball functions as a mouse-like device.

Configuration:
- Device type must be set appropriately in RetroArch
- Sensitivity may require tuning per game

Reference configurations (known working):
- Golden Tee
- Centipede

Networking
----------

Architecture
^^^^^^^^^^^^

- MikroTik router operates in **station mode**
- Connects to school WiFi
- Provides NAT for internal devices

Internal network:
- Raspberry Pi connects via Ethernet
- Access hatch exposes Ethernet ports for direct access

Remote Access
^^^^^^^^^^^^^

Supported methods:

- SSH (command line access)
- SFTP (file transfer)
- Tailscale (remote VPN access)

Tailscale enables:
- Secure remote SSH
- Access to internal services (e.g., stats dashboard)

Web Interface
^^^^^^^^^^^^^

System stats are available at:

::

   http://<tailscale-ip>:5000

Accessible only when connected to the Tailscale network.

MikroTik Management
^^^^^^^^^^^^^^^^^^^

Configuration is performed via WinBox:

- Connect via Ethernet
- Use MAC-based discovery
- Credentials stored externally

Users are not expected to modify configuration beyond basic connectivity troubleshooting.

Operational Modes
-----------------

Kiosk Mode
^^^^^^^^^^

- Restricts user access to settings
- Prevents accidental misconfiguration

Unlock:
- Button combination (stored externally)

Re-enable:
- Through EmulationStation UI

System Control
^^^^^^^^^^^^^^

Supported operations:

- Restart game (RetroArch)
- Restart RetroArch
- Restart EmulationStation
- Reboot system

These can be triggered via:
- Keyboard (F1 menu)
- Controller hotkeys
- CLI

Maintenance and Recovery
-----------------------

SD Card Recovery
^^^^^^^^^^^^^^^^

Recovery methods include:

- Booting into root shell via ``cmdline.txt``
- Mounting SD card externally
- Repairing permissions (e.g., restoring sudo)

This is critical due to:
- Filesystem corruption risk
- Improper shutdowns

Configuration Management
^^^^^^^^^^^^^^^^^^^^^^^^

- System configs stored in various locations
- EmulationStation settings stored in XML
- RetroArch configs layered (global → core → game)

Backups are strongly recommended before changes.

Display Configuration
^^^^^^^^^^^^^^^^^^^^^

Underscanning is handled via:

- EmulationStation config (primary)
- Framebuffer settings (secondary)

This ensures proper fit within the cabinet bezel.

Deprecated Subsystem: Barcode Scanner
-------------------------------------

Overview
^^^^^^^^

A secondary system was developed to control access via barcode scanning.

Status:
- Deprecated
- Not recommended for use

Reasons:
- Legal ambiguity
- Reliability concerns
- Complexity vs benefit

Architecture
^^^^^^^^^^^^

- Separate Raspberry Pi Zero 2 W
- USB barcode scanner input
- Python-based validation system
- Relay-triggered "coin insert" signal

Validation flow:

1. Scan barcode
2. Check whitelist
3. Check special codes
4. Validate format via regex
5. Check blacklist
6. Check daily usage limits
7. Trigger relay if allowed

All interactions are logged.

Web Interface
^^^^^^^^^^^^^

- Flask-based dashboard
- Allows:
  - Log viewing
  - Config editing (whitelist/blacklist)

File Structure
^^^^^^^^^^^^^^

::

   barcode_system/
   ├── barcode_scanner.py
   ├── config/
   │   ├── whitelist.txt
   │   ├── blacklist.txt
   │   └── settings.json
   ├── logs/
   └── utils/

Conclusion
----------

This arcade system balances usability, flexibility, and maintainability through:

- Modular hardware design
- Layered software configuration
- Secure remote access via Tailscale
- Controlled user interaction via kiosk mode

However, it requires:

- Careful handling of configuration changes
- Awareness of system fragility (SD card, RetroPie)
- Respect for physical and electrical constraints

The system is functional and extensible, but not idiot-proof. Misconfiguration or careless handling can break it quickly.
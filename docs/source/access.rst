Access Hatch
============

Overview
--------

The access hatch provides entry to core infrastructure components:

- Mechanical timer (screen and lighting)
- USB hub for RetroPie
- Ethernet ports (network access)

Opening the Hatch
-----------------

1. Use the designated key.
2. Unlock and open the hatch.

Internal Components
-------------------

Mechanical Timer
^^^^^^^^^^^^^^^^

- Controls power schedule for screen and lighting.
- Uses:
  - Rotating dial to set current time
  - Physical pins to define ON/OFF periods

Operation:
- Set the dial to current time.
- Adjust pins for desired schedule.

Override Switch:
- Located on the side.
- Forces **always-on mode**.

**Important:**
- Only use always-on in special circumstances.
- Leaving the system on continuously increases:
  - Screen burn-in risk
  - Fire risk
  - Component wear

USB Hub
^^^^^^^

- Connected directly to the Raspberry Pi.
- Provides USB expansion for:
  - Controllers
  - Encoders
  - Input devices

Ethernet Ports
^^^^^^^^^^^^^^

- Connected to the internal MikroTik router.
- Used for:
  - Direct network access
  - Troubleshooting
  - WinBox configuration

Safety Notes
------------

- Low-voltage components are generally safe to handle.
- **Do not interact with any AC power wiring.**
- Avoid forcing connections or pulling cables aggressively.
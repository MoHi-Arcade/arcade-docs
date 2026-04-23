Button Panel and Internal Hardware
=================================

Accessing the Button Panel
---------------------------

The button panel is secured from the front using spring-loaded pins.

Steps:

1. Remove the back panel of the arcade.
2. Locate the two spring-loaded pins at the front underside of the button panel.
3. Compress/release the pins.
4. Lift or remove the panel.

Internal Layout
---------------

Under the button panel:

- Raspberry Pi (RetroPie system)
- USB encoders (for buttons and joysticks)
- Power distribution system for button lighting

Raspberry Pi
^^^^^^^^^^^^

- Mounted using two bolts.
- Bolts are not backed by nuts; avoid applying stress.
- Powers:
  - System
  - USB hub

USB Encoders
^^^^^^^^^^^^

- Each encoder handles button and joystick inputs.
- Connected via USB to the Pi.

Button Wiring
^^^^^^^^^^^^^

Each button has two distinct electrical systems:

Switch Contacts (Input)
~~~~~~~~~~~~~~~~~~~~~~~

- Located inside the **grey box** on the button.
- Responsible for input signals to the encoder.

Backlight Power
~~~~~~~~~~~~~~~

- Terminals on the **side of the button**.
- Clearly labeled with polarity (+/-).

Power Distribution
------------------

- Backlighting power is distributed via **busbars**.
- Quick connections use **Anderson Powerpole connectors**.

Purpose:
- Fast connect/disconnect of button assemblies.
- Modular maintenance.

Safety Notes
------------

- System is primarily **5V low voltage**.
- Safe for general handling during maintenance.

However:

- AC power sections exist elsewhere in the cabinet.
- Do not interact with any exposed AC wiring.

General Guidance
----------------

- Do not pull on wires; disconnect via connectors.
- Maintain polarity when reconnecting lighting.
- Ensure all USB connections are secure before closing.

If something does not match expectations, stop and verify before proceeding.
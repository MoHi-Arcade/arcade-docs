Underscanning EmulationStation on RetroPie
==========================================

Overview
--------
Many arcade cabinets using RetroPie have screens larger than the visible cabinet window. This can cause EmulationStation (ES) and games to be partially cut off due to overscan. This guide explains how to configure ES and the Raspberry Pi to underscan the display, ensuring the image fits properly inside the cabinet bezel.

Raspberry Pi Console vs EmulationStation
----------------------------------------
- **Console (CLI)**: Uses the framebuffer set in `/boot/config.txt`. Overscan adjustments here only affect the command line interface.
- **EmulationStation (ES)**: Uses its own internal resolution and scaling settings. Adjustments here affect games and the ES UI.

Step 1: Editing EmulationStation Settings
------------------------------------------
1. Open the ES settings file:

   .. code-block:: bash

       sudo nano /opt/retropie/configs/all/emulationstation/es_settings.cfg

2. Locate the `<settings>` block. If it does not exist, create it:

   .. code-block:: xml

       <settings>
       </settings>

3. Add or modify the following entries to define the visible screen area:

   .. code-block:: xml

       <Int name="ScreenWidth">800</Int>
       <Int name="ScreenHeight">600</Int>
       <Bool name="Fullscreen">true</Bool>
       <Int name="ScreenRatio">1</Int>  <!-- 1 = 4:3, 0 = auto -->

   - **ScreenWidth** and **ScreenHeight** should match the visible window inside your cabinet bezel.
   - **Fullscreen** ensures ES covers the framebuffer.
   - **ScreenRatio** maintains a 4:3 aspect ratio for arcade games.

4. Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`) and restart ES:

   .. code-block:: bash

       emulationstation

Step 2: Adjusting Framebuffer (Optional)
----------------------------------------
For finer control, you can adjust the framebuffer in `/boot/config.txt`:

1. Edit the config file:

   .. code-block:: bash

       sudo nano /boot/config.txt

2. Add or modify the framebuffer size:

   .. code-block:: text

       framebuffer_width=1024
       framebuffer_height=768

3. Save, exit, and reboot:

   .. code-block:: bash

       sudo reboot

Step 3: Testing and Fine-Tuning
--------------------------------
- Launch EmulationStation and check if the visible image fits the cabinet window.
- Adjust `ScreenWidth`, `ScreenHeight`, and optionally `framebuffer_width`/`height` in small increments until the display fits correctly.
- For 4:3 arcade content on widescreen monitors, ensure `ScreenRatio=1` to prevent stretching.

Notes
-----
- Some RetroPie builds may still offer a "Screen Adjust" option in the ES UI (`UI Settings` → `Screen Adjust`), but this is not available on all versions. Manual config file edits are the most reliable method.
- Always back up `es_settings.cfg` before making changes.

References
----------
- Official RetroPie Documentation: https://retropie.org.uk/docs/
- Raspberry Pi Configuration: https://www.raspberrypi.com/documentation/computers/config_txt.html
Games Management
================

Adding Games
------------

Games can be added via SFTP or CLI.

**SFTP Method**
1. Connect to the Pi using an SFTP client.
2. Navigate to:
   /home/pi/RetroPie/roms/<system>
3. Upload ROM files into the appropriate system folder.
4. Restart EmulationStation (see Restarting section).

**CLI Method**
1. SSH into the Pi.
2. Copy files:
   scp <file> pi@<pi-ip>:/home/pi/RetroPie/roms/<system>/
3. Restart EmulationStation.

Deleting Games
--------------

**SFTP**
- Delete the ROM file from the corresponding system folder.

**CLI**
- SSH into the Pi:
  rm /home/pi/RetroPie/roms/<system>/<rom>

Renaming Games
--------------

- Rename the ROM file directly via SFTP or CLI:
  mv oldname.zip newname.zip

- If metadata does not update:
  - Delete corresponding file in:
    /home/pi/.emulationstation/gamelists/<system>/gamelist.xml
  - Restart EmulationStation

Notes
-----
- ROM names affect how games are displayed.
- Scraper may need to be re-run for proper metadata.
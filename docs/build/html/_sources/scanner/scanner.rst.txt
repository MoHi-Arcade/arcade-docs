Barcode Scanner [Deprecated]
=====================================

Overview
--------
This documentation covers the setup, operation, and maintenance of the Raspberry Pi Barcode Scanning System.

This system was built originally to control access and limit the amount of plays per person per day
Due to a number of issues, it was never used outside of testing
We don't recommend using this feature due to iffy legality mumbo jumbo
The barcode scanner system is connected to a raspberrypi 0wh2
It runs raspberrypi lite and runs several custom python scripts
The it works is when a barcode is scanned, it checks it against a whitelist and a list of special codes
Then, if it doesn't find a match in either of those, it will then check it against a regex, to see if it matches the format of a student ID
If it does, then it'll check it against the blacklist, if it does not match, it will check against the log to see how many time the student has played in the last day
If it below the set threshold it will trigger a relay that triggers a coin to be entered in the RetroPie
All interactions are logged including failed attempts,
The other script running on the RaspberryPi is a simple Flask app that powers a web-board to let the user view the logs and edit the blacklist, whitelist, and special codes

Contents:
- `installation`
- `configuration`
- `usage`
- `file_structure`
- `troubleshooting`
- `development`

.. toctree::
   :maxdepth: 2
   :caption: Pages

   installation
   configuration
   usage
   file_structure
   troubleshooting
   development


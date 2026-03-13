Troubleshooting
===============

Problem: Whitelist/Blacklist Not Loading
----------------------------------------
- Ensure file paths are correct in `settings.json`.
- Confirm file permissions allow the script to read them:

  .. code-block:: bash

     chmod 644 config/whitelist.txt
     chmod 644 config/blacklist.txt

Problem: Scanner Input Not Detected
-----------------------------------
- Verify USB connection.
- Test with `lsusb` to ensure the device is recognized.
- Ensure the scanner outputs in the correct keyboard/input mode.

Problem: Logs Not Created
-------------------------
- Check `logs/` directory permissions.
- Confirm `settings.json` has logging enabled.
Configuration
=============

Whitelist and Blacklist
-----------------------
- `whitelist.txt` – List of allowed barcode IDs.
- `blacklist.txt` – List of disallowed barcode IDs.
- Each entry must be on a separate line.
- Files are located in the `config/` directory.

Other Configuration Files
-------------------------
- `settings.json` – JSON file storing system-wide options like logging preferences and scan modes.
- `logs/` – Directory for storing scan logs.

Tips for Maintaining Configurations
-----------------------------------
- Always backup `whitelist.txt` and `blacklist.txt` before editing.
- Validate JSON files using online tools or `python -m json.tool`.
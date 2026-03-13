File Structure
==============

barcode_system/
├── barcode_scanner.py    # Main Python script
├── config/
│   ├── whitelist.txt
│   ├── blacklist.txt
│   └── settings.json
├── logs/                 # Scan log files
└── utils/                # Optional helper scripts

Notes
-----
- The main script imports modules from `utils/` for modularity.
- Keep the config directory readable/writable by the Pi user.
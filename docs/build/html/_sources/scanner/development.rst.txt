Development
===========

Code Overview
-------------
- `barcode_scanner.py`
  - Main loop handling input and validation.
  - Imports: `json`, `datetime`, `re`, `os`
- `utils/`
  - Helper functions for file I/O, formatting, or additional validation.

Adding Features
---------------
- New validation rules: modify `utils/validators.py`.
- Network logging: implement in `utils/network_logger.py`.
- Update documentation when adding new config options.

Testing
-------
- Run the script with a test barcode set before deployment.
- Use small log files to avoid overwhelming the system during tests.
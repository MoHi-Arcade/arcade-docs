Usage
=====

Starting the Scanner
-------------------
Run the main script:

.. code-block:: bash

   ./barcode_scanner.py

Behavior
--------
1. The system waits for barcode input from the USB scanner.
2. Upon scanning, it checks the barcode against:
   - `whitelist.txt` → If matched, marks as allowed.
   - `blacklist.txt` → If matched, marks as denied.
3. Unknown barcodes are logged for review.

Logging
-------
- All scans are recorded in `logs/YYYY-MM-DD.log`.
- Each entry includes:
  - Timestamp
  - Barcode value
  - Validation result (whitelisted, blacklisted, unknown)
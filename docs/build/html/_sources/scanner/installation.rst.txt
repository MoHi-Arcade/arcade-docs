Installation
============

Hardware Requirements
---------------------
- Raspberry Pi 3 or 4
- USB Barcode Scanner
- SD Card (16GB or larger)
- Network connectivity for optional logging

Software Requirements
---------------------
- Raspberry Pi OS (64-bit recommended)
- Python 3.9+
- Python packages:
  - json
  - datetime
  - re

Installation Steps
------------------
1. Flash Raspberry Pi OS onto SD card.
2. Connect the barcode scanner to USB.
3. Clone the barcode system repository:
   .. code-block:: bash

      git clone <repo_url> ~/barcode_system

4. Install Python dependencies:
   .. code-block:: bash

      pip install -r ~/barcode_system/requirements.txt

5. Ensure the main script is executable:
   .. code-block:: bash

      chmod +x ~/barcode_system/barcode_scanner.py
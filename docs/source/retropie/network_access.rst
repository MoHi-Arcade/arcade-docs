Network Access (SSH, SFTP, Tailscale)
======================================

SSH Access
----------

1. Ensure SSH is enabled:
   sudo raspi-config
   → Interface Options → SSH → Enable

2. Connect:
   ssh pi@<pi-ip>

SFTP Access
-----------

Use any SFTP client:
- Host: <pi-ip>
- User: pi
- Password: (see Google Doc)

Directory:
  /home/pi/RetroPie/

Tailscale Usage
---------------

Connecting to Pi
----------------

1. Ensure Pi is connected to Tailscale:
   tailscale status

2. Note Tailscale IP.

3. SSH:
   ssh pi@<tailscale-ip>

Installing Tailscale on Personal Devices
----------------------------------------

Mac:
  brew install tailscale

Windows:
  Download from Tailscale website and install.

Linux:
  curl -fsSL https://tailscale.com/install.sh | sh

iPhone:
  Install from App Store.

Login:
- Use same account as Pi.

Notes
-----
- Devices must be on same Tailscale network.
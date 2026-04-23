Web Interface (System Stats)
===========================

Accessing Stats Dashboard
--------------------------

1. Connect to Tailscale network.
2. Open browser.
3. Navigate to:
   http://<tailscale-ip>:5000

Notes
-----
- Service must be running on the Pi.
- If inaccessible:
  - Verify Tailscale connection
  - Check service:
    sudo systemctl status <service-name>

Security
--------
- Only accessible via Tailscale network.
- Do not expose publicly.
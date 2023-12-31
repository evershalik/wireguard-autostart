# wireguard-autostart

### Autostart WireGuard in systemd
These steps are mostly distribution agnostic and have been tested on Debian unstable and Fedora.

1. Generate a valid and working WireGuard configuration file `/etc/wireguard/wg0.conf`. Our setup guide offers details.

>Note: You may have to replace the Endpoint hostname with the WireGuard server IP address in the WireGuard configuration file. DNS may or may not be applied when systemd brings the wg0 interface up.

2. Add the WireGuard service to systemd:
```patch
sudo systemctl enable wg-quick@wg0.service
sudo systemctl daemon-reload
```

3. Start the new service immediately:
```patch
sudo systemctl start wg-quick@wg0
```

4. Reboot your computer system to verify the automatic connection on startup works as expected.

5. Check the service status:
```
systemctl status wg-quick@wg0
```

6. To remove the service and clean up the system:
```patch
sudo systemctl stop wg-quick@wg0
sudo systemctl disable wg-quick@wg0.service
sudo rm -i /etc/systemd/system/wg-quick@wg0*
sudo systemctl daemon-reload
sudo systemctl reset-failed
```

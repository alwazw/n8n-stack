# Host Configuration Instructions for n8n-stack

## Updating /etc/hosts

To ensure your system can resolve the hostname `n8n-stack` to the correct IP addresses, you need to update your `/etc/hosts` file.

1. Open the hosts file with sudo privileges:
   ```
   sudo nano /etc/hosts
   ```

2. Add the following lines to the file:
   ```
   192.168.2.104 n8n-stack
   10.10.10.104 n8n-stack
   ```

3. Save the file and exit (Ctrl+O, Enter, Ctrl+X in nano)

## Updating /etc/resolv.conf

To ensure proper DNS resolution, you may need to update your `/etc/resolv.conf` file.

1. Open the resolv.conf file with sudo privileges:
   ```
   sudo nano /etc/resolv.conf
   ```

2. Ensure it contains the following entries (keeping your existing nameservers):
   ```
   nameserver 127.0.0.53
   nameserver 1.1.1.1
   options edns0 trust-ad
   search home
   ```

3. Save the file and exit (Ctrl+O, Enter, Ctrl+X in nano)

## Important Notes

- On many systems, `/etc/resolv.conf` is managed by systemd-resolved or other services and may be overwritten on reboot
- For permanent changes, consider updating your network configuration files or using `resolvconf`
- If using NetworkManager, you can add DNS settings through its configuration

## Testing the Configuration

After updating the files, test that the hostname resolves correctly:

```
ping n8n-stack
```

You should see responses from either 192.168.2.104 or 10.10.10.104.

## Accessing n8n

Once the hostname is properly configured, you can access n8n at:
- https://n8n-stack/

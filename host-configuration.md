# Cross-Platform Host Configuration for n8n-stack

This guide provides instructions for configuring hostname resolution on both Windows and Linux systems to access your n8n stack.

## Windows Configuration

### Updating Hosts File

1. Open Notepad as Administrator:
   - Search for "Notepad" in the Start menu
   - Right-click on Notepad and select "Run as administrator"
   - Click "Yes" on the UAC prompt

2. Open the hosts file:
   - In Notepad, go to File > Open
   - Navigate to: `C:\Windows\System32\drivers\etc\`
   - Change the file filter from "Text Documents (*.txt)" to "All Files (*.*)"
   - Select the file named "hosts" and click Open

3. Add these lines at the end of the file:
   ```
   192.168.2.104 n8n-stack
   10.10.10.104 n8n-stack
   ```

4. Save the file (File > Save)

5. Test the configuration:
   ```
   ping n8n-stack
   ```

### Troubleshooting Windows Hostname Resolution

If hostname resolution isn't working:

1. Flush DNS cache:
   ```
   ipconfig /flushdns
   ```

2. Check if the hosts file has correct permissions:
   - Right-click on the hosts file
   - Select Properties
   - Ensure it's not set to Read-only

3. Try accessing by IP address directly to verify connectivity:
   ```
   ping 192.168.2.104
   ```

## Linux Configuration

### Updating Hosts File

1. Open the hosts file with sudo privileges:
   ```
   sudo nano /etc/hosts
   ```

2. Add the following lines:
   ```
   192.168.2.104 n8n-stack
   10.10.10.104 n8n-stack
   ```

3. Save the file and exit (Ctrl+O, Enter, Ctrl+X in nano)

4. Test the configuration:
   ```
   ping n8n-stack
   ```

### Updating resolv.conf (if needed)

On many Linux systems, `/etc/resolv.conf` is managed by systemd-resolved or other services. For permanent changes:

1. If using systemd-resolved, edit the resolved.conf file:
   ```
   sudo nano /etc/systemd/resolved.conf
   ```

2. Uncomment and modify the DNS line:
   ```
   [Resolve]
   DNS=1.1.1.1 8.8.8.8
   ```

3. Restart the service:
   ```
   sudo systemctl restart systemd-resolved
   ```

### Troubleshooting Linux Hostname Resolution

If hostname resolution isn't working:

1. Flush DNS cache:
   ```
   sudo systemd-resolve --flush-caches
   ```

2. Check DNS resolution:
   ```
   resolvectl status
   ```

3. Try accessing by IP address directly to verify connectivity:
   ```
   ping 192.168.2.104
   ```

## Accessing n8n

After configuring hostname resolution, you can access n8n at:
- https://n8n-stack/

For handling certificate warnings, see the [Certificate Trust Guide](certificate-trust-guide.md).

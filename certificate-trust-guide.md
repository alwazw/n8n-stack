# Trusting Self-Signed Certificates

When accessing your n8n stack via HTTPS with a self-signed certificate, your browser will show security warnings. This document explains how to trust the certificate on different browsers and operating systems.

## Windows

### Chrome / Edge

1. Navigate to https://n8n-stack/
2. You'll see a warning page "Your connection is not private" or similar
3. Click on "Advanced" or "Details"
4. Click on "Proceed to n8n-stack (unsafe)" link at the bottom
5. To permanently trust the certificate:
   - Click on the padlock icon in the address bar
   - Click on "Certificate (Invalid)"
   - Click on "Certificate details" or "Details"
   - Click on "Export" or "Copy to File"
   - Save the certificate to your desktop
   - Double-click the saved certificate file
   - Select "Install Certificate"
   - Select "Current User" and click "Next"
   - Select "Place all certificates in the following store"
   - Click "Browse" and select "Trusted Root Certification Authorities"
   - Click "Next" and then "Finish"
   - Restart your browser

### Firefox

1. Navigate to https://n8n-stack/
2. You'll see a warning page "Warning: Potential Security Risk Ahead"
3. Click on "Advanced..."
4. Click on "Accept the Risk and Continue"
5. To permanently trust the certificate:
   - Click on the padlock with the warning icon in the address bar
   - Click on the right arrow (>) next to "Connection not secure"
   - Click on "More Information"
   - Click on "View Certificate"
   - Click on "Export..."
   - Save the certificate to your desktop
   - Go to Firefox Options/Preferences
   - Search for "certificates" and click on "View Certificates"
   - Go to the "Authorities" tab
   - Click "Import" and select the saved certificate file
   - Check "Trust this CA to identify websites" and click "OK"
   - Restart Firefox

## Linux

### Chrome / Chromium

1. Navigate to https://n8n-stack/
2. Follow the same steps as Chrome on Windows to temporarily proceed
3. To permanently trust the certificate system-wide:
   - Export the certificate as described in the Windows section
   - Open terminal and run:
     ```
     sudo mkdir -p /usr/local/share/ca-certificates/extra
     sudo cp /path/to/exported/certificate.crt /usr/local/share/ca-certificates/extra/n8n-stack.crt
     sudo update-ca-certificates
     ```
   - Restart Chrome/Chromium

### Firefox on Linux

1. Follow the same steps as Firefox on Windows

## Exporting the Certificate from the Server

If you prefer to export the certificate directly from your server:

1. SSH into your server
2. Run the following command:
   ```
   sudo cp /home/ubuntu/n8n-stack/nginx/certs/n8n-stack.crt ~/
   sudo chmod 644 ~/n8n-stack.crt
   ```
3. Use SCP or another file transfer method to copy the certificate to your local machine:
   ```
   scp username@server-ip:~/n8n-stack.crt /local/path/
   ```
4. Follow the browser-specific instructions above to import the certificate

## Troubleshooting

If you still encounter certificate issues after following these steps:

1. Ensure your system time is correct (certificate validation depends on accurate time)
2. Clear your browser cache and cookies
3. Try accessing the site in an incognito/private window
4. Check that the certificate's Common Name (CN) matches the hostname you're using
5. Verify that the certificate hasn't expired

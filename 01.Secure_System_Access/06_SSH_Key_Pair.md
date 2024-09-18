# 02 - Scenario: Setting Up Secure SSH Access for a Remote Server

### Introduction
In this scenario, we will set up secure SSH access for a remote server using key-based authentication. SSH keys provide a more secure method of logging into a server compared to password-based authentication. We will cover the process of generating an SSH key pair, copying the public key to the remote server, verifying that key-based authentication works, and optionally securing the server further by disabling password authentication.

### Practical
```bash
# Step 1: Generate the SSH Key Pair
# Create a new SSH key pair with a 4096-bit RSA key
# The -C option adds a label (email) to the key for identification
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Step 2: Copy the Public Key to the Remote Server
# Use ssh-copy-id to copy the public key to the remote server's authorized_keys
# This allows key-based authentication without requiring a password
ssh-copy-id username@remote_server_ip

# If ssh-copy-id is not available, manually copy the public key using scp
# This copies the public key file to the remote server and appends it to authorized_keys
# Ensure the destination directory and file exist on the remote server
scp ~/.ssh/id_rsa.pub username@remote_server_ip:~/.ssh/authorized_keys

# Step 3: Verify SSH Key Authentication
# Attempt to log in to the remote server to verify key-based authentication
# If configured correctly, you should log in without a password prompt
ssh username@remote_server_ip

# If you encounter issues with authentication, check and set the correct permissions
# The .ssh directory should be accessible only by the user
chmod 700 ~/.ssh
# The authorized_keys file should be readable and writable only by the user
chmod 600 ~/.ssh/authorized_keys

# Step 4: Secure the Server (Optional)
# To enhance security, disable password-based logins
# Edit the SSH configuration file to disable password authentication
sudo nano /etc/ssh/sshd_config
# Locate and set PasswordAuthentication to no
# Save the file and exit the editor
# Restart the SSH service to apply changes
sudo systemctl restart sshd

```
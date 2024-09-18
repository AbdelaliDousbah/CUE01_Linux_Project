# User Accounts Management

### Introduction
Managing user accounts is a fundamental aspect of system administration. It involves creating, modifying, deleting, and managing user accounts and groups. Proper user account management ensures secure and organized access to system resources.

### Practical

```bash
# Step 1: Creating User Accounts
# Create a new user account with the username 'alice'
# -m: Create the user's home directory
# -s: Set the default shell for the user
useradd -m -s /bin/bash alice

# Create a user account with a custom home directory and default shell
# -d: Specify a custom home directory
# -s: Set the default shell
useradd -m -d /custom/home/alice -s /bin/zsh alice2

# Add a user with a specific user ID (UID)
# -u: Set a custom UID
useradd -m -u 1501 -s /bin/bash bob

# Create a user with a specific group
# -g: Set the primary group for the user
useradd -m -g developers -s /bin/bash carol

# Create a user with multiple supplementary groups
# -G: Add the user to additional groups
useradd -m -G sudo,admin -s /bin/bash dave

# Step 2: Modifying User Accounts
# Modify the user account 'alice'
# -c: Set a comment (usually the full name)
# -G: Add the user to additional groups
usermod -c "Alice Johnson" -G sudo,developers alice

# Change the user's default shell to /bin/zsh
usermod -s /bin/zsh alice

# Lock a user account to prevent login
# -L: Lock the user account
usermod -L alice

# Unlock the user account
# -U: Unlock the user account
usermod -U alice

# Change the user's home directory
# -d: Specify a new home directory
# -m: Move the contents of the old home directory to the new location
usermod -d /new/home/directory -m alice

# Step 3: Deleting User Accounts
# Delete a user account and remove the home directory
# -r: Remove the user's home directory and mail spool
userdel -r alice

# Delete a user without removing the home directory
userdel bob

# Step 4: Managing User Groups
# Create a new group called 'developers'
groupadd developers

# Create a group with a specific GID
# -g: Set a custom GID
groupadd -g 1501 dev_team

# Add a user to a group
# -aG: Append the user to the specified group
usermod -aG developers carol

# Remove a user from a group
# Use gpasswd to remove a user from a group
gpasswd -d carol developers

# Delete a group
# groupdel: Remove the specified group
groupdel oldgroup

# Step 5: Setting User Permissions
# Change the ownership of a file to a specific user and group
# chown: Set the user and group ownership of a file
chown alice:developers /path/to/file

# Change file permissions
# chmod: Set read, write, and execute permissions
# 755: Owner has full permissions, group and others have read and execute permissions
chmod 755 /path/to/file

# Grant write permissions to a group
# 775: Owner and group have full permissions, others have read and execute permissions
chmod 775 /path/to/directory

# Set permissions recursively on a directory
# -R: Apply changes to all files and directories within
chmod -R 700 /path/to/directory
```
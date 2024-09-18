# Group Membership

### Introduction
In Linux, groups are used to organize and manage user permissions for files, directories, and system resources. Each user can belong to multiple groups, and groups can be used to grant access to specific resources without modifying individual user permissions.

There are two main types of groups:
- **Primary group**: The group associated with the user's account.
- **Secondary groups**: Additional groups that the user is a member of.

Managing group membership is essential for system administrators to control access to system resources, enforce policies, and manage permissions efficiently.

### Practical
```bash
# Step 1: Creating a new group
# Use the groupadd command to create a new group.
groupadd developers

# Step 2: Adding a user to a group
# Add a user to a secondary group (without affecting the primary group).
usermod -aG developers alice

# Step 3: Viewing group membership
# To view the groups a user is a member of, use the groups command.
groups alice
# Alternatively, you can use the id command to display both the user's UID and GID.
id alice

# Step 4: Changing the primary group of a user
# Use the usermod command to change a user's primary group.
usermod -g developers bob

# Step 5: Removing a user from a group
# To remove a user from a secondary group, use the gpasswd command.
gpasswd -d alice developers

# Step 6: Managing group memberships via /etc/group
# The /etc/group file stores group information. You can manually edit it to adjust group memberships.
# Here's an example of the /etc/group file format:
# group_name:x:GID:user1,user2,user3
# Example:
developers:x:1001:alice,bob

# Step 7: Creating a group with a specific GID
# Use the -g option to specify the GID when creating a group.
groupadd -g 1050 project_team

# Step 8: Deleting a group
# To delete a group from the system.
groupdel project_team

# Step 9: Adding multiple users to a group
# You can add multiple users to a group by listing them with usermod.
usermod -aG developers dave
usermod -aG developers carol

# Step 10: Assigning administrative tasks with groups
# Create an admin group and give it sudo privileges by editing the sudoers file with visudo.
groupadd admin
usermod -aG admin alice
# Grant the admin group sudo access in the /etc/sudoers file:
%admin ALL=(ALL:ALL) ALL
```

# Key Points
- Primary groups are assigned to users at creation, while secondary groups can be added later.
- Group membership can be managed with commands like `usermod`, `gpasswd`, and directly through `/etc/group`.
- The `-aG` option with `usermod` ensures users are added to secondary groups without losing current group memberships.
- Group-based access is an efficient way to manage permissions for multiple users.
- Groups can also be assigned special privileges, such as sudo access, via the `/etc/sudoers` file.

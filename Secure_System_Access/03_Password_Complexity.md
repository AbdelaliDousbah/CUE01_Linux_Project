# Password Complexity

### Introduction
Password complexity is essential to maintaining the security of Linux systems. It involves enforcing rules that make passwords harder to guess or crack, such as requiring a combination of uppercase, lowercase, numeric, and special characters, as well as enforcing password length and expiration policies.

In Linux, password complexity can be managed using:

- **PAM (Pluggable Authentication Modules)**: Used to enforce password policies such as strength, complexity, and password history.
- **/etc/login.defs**: This file defines system-wide password policies, including aging, minimum length, and expiration warnings.
- **chage**: A command-line tool used to manage password aging policies on a per-user basis.
- **passwd**: A tool to change user passwords, force expiration, or lock accounts.

### Practical
```bash
# Step 1: Enforce Password Complexity using PAM
# In the file `/etc/pam.d/common-password`, use the `pam_pwquality.so` module to enforce password policies.

# Example configuration in /etc/pam.d/common-password:
# retry=3: Allows the user to try three times to meet the complexity requirements.
# minlen=12: Sets the minimum password length to 12 characters.
# dcredit=-1: Requires at least one digit.
# ucredit=-1: Requires at least one uppercase letter.
# lcredit=-1: Requires at least one lowercase letter.
# ocredit=-1: Requires at least one special character.
password requisite pam_pwquality.so retry=3 minlen=12 dcredit=-1 ucredit=-1 lcredit=-1 ocredit=-1

# Step 2: Configure Password Policies with login.defs
# The `/etc/login.defs` file allows you to configure system-wide password policies.

# Example settings in `/etc/login.defs`:
# PASS_MAX_DAYS: The maximum number of days a password is valid (e.g., 90 days).
# PASS_MIN_DAYS: The minimum number of days between password changes (e.g., 1 day).
# PASS_MIN_LEN: The minimum password length (e.g., 12 characters).
# PASS_WARN_AGE: The number of days before expiration to warn users (e.g., 7 days).

# Example:
PASS_MAX_DAYS 90
PASS_MIN_DAYS 1
PASS_MIN_LEN 12
PASS_WARN_AGE 7

# Step 3: Set Password Aging and Expiry with chage
# Use `chage` to set password aging and expiration policies for individual users.

# Set a password to expire after 90 days
chage -M 90 alice

# Force a user to change the password at next login
chage -d 0 alice

# Set a warning period of 7 days before password expiration
chage -W 7 alice

# View a user's current password expiration and aging settings
chage -l alice

# Step 4: Enforcing Password History
# Prevent users from reusing their last 5 passwords by modifying `/etc/pam.d/common-password`.

# Example configuration to enforce password history:
# remember=5: Ensures users cannot reuse their last 5 passwords.
password sufficient pam_unix.so remember=5

# Step 5: Using passwd Command for Immediate Password Updates
# Force a user to change their password with the `passwd` command.
passwd alice

# Set a password expiration immediately for a specific user.
passwd -e bob

# Disable an account by locking the password, preventing login.
passwd -l carol

# Unlock a user account after being locked.
passwd -u carol

# Change the password for a user interactively.
passwd dave
```
# Key Points
- PAM (`/etc/pam.d/common-password`) is used for enforcing password complexity, length, and history.
- `login.defs` provides system-wide configuration for password expiration, minimum length, and aging policies.
- `chage` is useful for managing individual user password expiration policies.
- `passwd` provides a quick way to update, lock, or expire user passwords.
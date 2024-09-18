# Creating Directories in Linux

## 1. Basic Directory Creation

- **`mkdir my_directory`**
  - **Description**: Creates a single directory named `my_directory`.
  - **Usage**: Use this command to create a simple directory.
  - **Verification**: Run `ls -l` to check if `my_directory` has been created.

## 2. Creating Multiple Directories

- **`mkdir dir1 dir2 dir3`**
  - **Description**: Creates three directories named `dir1`, `dir2`, and `dir3`.
  - **Usage**: Useful for creating several directories at once.
  - **Verification**: Run `ls -l` to see the new directories listed.

- **`mkdir -p parent/child/child2`**
  - **Description**: Creates a directory structure where `parent` is the parent directory, and `child` and `child2` are subdirectories within it. The `-p` option ensures that intermediate directories are created as needed.
  - **Usage**: Use this to create nested directories in one command.
  - **Verification**: Run `ls -R` to see the full directory tree.

## 3. Using Braces to Create Multiple Directories

- **`mkdir ubuntu{16,18,20,22,24}{LTS,DEV}`**
  - **Description**: Creates directories with a combination of years and labels. This will create directories like `ubuntu16LTS`, `ubuntu18LTS`, `ubuntu20LTS`, etc.
  - **Usage**: Efficient for creating directories with different combinations of names.
  - **Verification**: Run `ls -l` to check all the created directories.

## 4. Creating Directories with Permissions

- **`mkdir -m 755 my_secure_directory`**
  - **Description**: Creates a directory named `my_secure_directory` with `755` permissions, which allows read, write, and execute permissions for the owner and read and execute permissions for others.
  - **Usage**: Use this command when you need to set specific permissions during directory creation.
  - **Verification**: Run `ls -ld my_secure_directory` to check the permissions.

## 5. Creating Directories with Parent Directories

- **`mkdir -p /var/www/html/{site1,site2}`**
  - **Description**: Creates multiple directories (`site1` and `site2`) under the `/var/www/html` path. The `-p` option ensures that `/var/www/html` is created if it does not already exist.
  - **Usage**: Useful for setting up a web server structure.
  - **Verification**: Run `ls -R /var/www/html` to see the created directories.

## 6. Creating Nested Directories

- **`mkdir -p /home/user/{Documents,Downloads/{Photos,Videos}}`**
  - **Description**: Creates a directory structure where `Documents` and `Downloads` are created under `/home/user`, with `Photos` and `Videos` nested inside `Downloads`.
  - **Usage**: Useful for organizing files into a hierarchy.
  - **Verification**: Run `ls -R /home/user` to see the nested structure.

## 7. Creating Directories with Spaces in Names

- **`mkdir "My Directory With Spaces"`**
  - **Description**: Creates a directory with spaces in its name.
  - **Usage**: Enclose the name in quotes to handle spaces.
  - **Verification**: Run `ls -l` to see the directory listed with spaces.

## 8. Creating a Directory and Moving into It

- **`mkdir my_new_dir && cd my_new_dir`**
  - **Description**: Creates a directory named `my_new_dir` and then immediately changes into it.
  - **Usage**: Combines directory creation and navigation in one command.
  - **Verification**: Run `pwd` to verify you are in `my_new_dir`.

## 9. Creating Directories from a File List

- **`xargs mkdir < directories.txt`**
  - **Description**: Creates directories listed in `directories.txt`. Each line in `directories.txt` should contain a directory name.
  - **Usage**: Efficient for creating a large number of directories from a file.
  - **Verification**: Run `ls -l` to check if all directories listed in `directories.txt` have been created.

## 10. Creating Directories with a Specific Owner

- **`sudo mkdir /opt/mydir && sudo chown user:user /opt/mydir`**
  - **Description**: Creates a directory `/opt/mydir` with `sudo` and then changes ownership to `user:user`.
  - **Usage**: Use this command when you need to create a directory with specific ownership.
  - **Verification**: Run `ls -ld /opt/mydir` to check the ownership and permissions.


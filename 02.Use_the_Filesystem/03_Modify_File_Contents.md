# Modify File Contents

### Introduction
Modifying file contents is essential for system administrators. Common tasks include appending, replacing, and editing without opening files. Key tools:
- **`echo`**: Append content.
- **`sed`**: Replace, insert, or delete lines.
- **`awk`**: Advanced text processing.
- **`truncate`**: Resize files.
- **`cat`**: Combine or append files.

These tools help automate file modifications efficiently.

### Practical
```bash
# Step 1: Appending text to a file
# Use echo with >> to append content to the end of a file.
echo "New log entry" >> /var/log/custom.log

# Step 2: Replacing text in a file with sed
# Replace all occurrences of "error" with "warning" in a log file.
sed -i 's/error/warning/g' /var/log/custom.log

# Step 3: Inserting a line before or after a specific pattern (sed)
# Insert a line before the line containing "server" in a config file.
sed -i '/server/i\# New server configuration' /etc/myapp/config.conf
# Insert a line after the match
sed -i '/server/a\# End of server configuration' /etc/myapp/config.conf

# Step 4: Delete lines matching a pattern (sed)
# Remove all lines containing "debug" from the configuration file.
sed -i '/debug/d' /etc/myapp/config.conf

# Step 5: Using awk to modify specific fields in a CSV file
# Update the second field (email) in a CSV when the first field (name) matches "John".
awk -F, '$1 == "John" {$2 = "john@example.com"}1' OFS=, file.csv > updated.csv

# Step 6: Truncate a file to a specific size
# Reduce a file size to 100MB (useful for log rotation).
truncate -s 100M /var/log/large.log

# Step 7: Append multiple files into one
# Combine multiple log files into a single file for easier analysis.
cat /var/log/custom.log /var/log/system.log /var/log/application.log > /var/log/all_logs.log

# Step 8: Batch replace in multiple files
# Replace "foo" with "bar" in all files under /etc/myapp.
find /etc/myapp/ -type f -exec sed -i 's/foo/bar/g' {} +

# Step 9: Use head/tail to modify specific parts of files
# Remove the first 10 lines of a file (tail can extract the remaining lines).
tail -n +11 oldfile.txt > newfile.txt

# Step 10: Edit a specific line number in a file
# Replace the 5th line of a file with new content.
sed -i '5s/.*/This is the new line content/' /etc/myapp/config.conf

# Step 11: Backup original files when modifying with sed
# Always create a backup before making changes.
sed -i.bak 's/foo/bar/g' /etc/myapp/config.conf

# Step 12: Modify a file’s permissions directly in-place
# Forcing file permission change after modification.
chmod 600 /etc/myapp/secure.conf

```

### Key Points
- **Appending**: Use `echo` or `cat` to append content to the end of a file.
- **Replacing text**: `sed` allows in-place editing of files, replacing patterns or specific text.
- **Inserting and deleting lines**: `sed` can insert lines before or after a match, and also delete lines.
- **Field-based edits**: `awk` is useful for modifying specific fields in structured data files (e.g., CSV).
- **Truncating files**: `truncate` can reduce file size without opening the file.
- **Combining files**: `cat` can merge multiple files into one, making log analysis easier.
- **Batch processing**: `find` combined with `sed` enables you to apply changes across multiple files.
- **Editing specific lines**: `sed` can modify or replace content at specific line numbers.
- **Creating backups**: When using `sed`, it's good practice to create backups with `-i.bak`.
- **File permissions**: Always ensure file permissions are correct, especially after modifications.

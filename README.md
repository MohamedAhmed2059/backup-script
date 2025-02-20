#!/bin/bash

# Prompt the user to enter the path of the file/folder to back up
echo "Enter the path of the file or folder you want to back up:"
read source_path

# Check if the provided path exists
if [ ! -e "$source_path" ]; then
    echo "Error: The specified path does not exist. Please check and try again!"
    exit 1
fi

# Ask the user where to save the backup
echo "Enter the destination directory for the backup:"
read backup_dir

# Ensure the backup directory exists (create it if necessary)
mkdir -p "$backup_dir"

# Generate a timestamp for the backup file name
timestamp=$(date +"%Y-%m-%d_%H-%M-%S")
backup_name="backup_$timestamp.tar.gz"

# Create the backup using tar and gzip
tar -czvf "$backup_dir/$backup_name" "$source_path"

# Verify if the backup was created successfully
if [ $? -eq 0 ]; then
    echo "Backup created successfully: $backup_dir/$backup_name"
else
    echo "Error: Failed to create the backup!"
fi

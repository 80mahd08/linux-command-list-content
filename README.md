
# lc

`lc` is a simple Bash script that recursively lists the contents of a directory. Files are displayed in green, and directories are displayed in blue, with subdirectories indented for clarity.

## Features

- **Recursive Directory Listing**: Automatically lists all files and subdirectories within a directory.
- **Colored Output**: Files are displayed in green, and directories in blue.
- **Indentation**: Subdirectories are indented to visually represent the directory structure.

## Installation

Follow these steps to download, install, and use `lc`:

### 1. Download the Script

Download the `lc` script using `curl`:

```bash
curl -o lc https://raw.githubusercontent.com/80mahd08/linux-command-list-content/main/lc

```

Or you can create the script manually:

```bash
nano lc
```

Then paste the following code into the `lc` file:

```bash
#!/bin/bash

# Function to display the contents of a directory recursively
display_contents() {
    local folder="$1"
    local indent="$2"

    # List all files and folders
    for item in "$folder"/*; do
        if [ -d "$item" ]; then
            # If it's a directory, print it in blue
            echo -e "${indent}\e[34m$(basename "$item")\e[0m"
            # Recursively call the function with increased indent
            display_contents "$item" "    $indent"
        elif [ -f "$item" ]; then
            # If it's a file, print it in green
            echo -e "${indent}\e[32m$(basename "$item")\e[0m"
        fi
    done
}

# Starting point of the script
start_folder="${1:-.}"

# Call the function with the initial folder and no indent
display_contents "$start_folder" ""
```

### 2. Make the Script Executable

Change the script's permissions to make it executable:

```bash
chmod +x lc
```

### 3. Move the Script to `/usr/bin`

To make the `lc` command available system-wide, move it to `/usr/bin`:

```bash
sudo mv lc /usr/bin/
```

### 4. Usage

Now you can use the `lc` command to list the contents of any directory. Simply navigate to the directory you want to list and run:

```bash
lc
```

Or specify a directory as an argument:

```bash
lc /path/to/directory
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

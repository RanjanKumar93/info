# Shells and Terminals

### **Ch 1. Terminals and Shells**
- **Terminal**: A terminal is an interface that allows users to interact with the shell by entering commands. Common terminals include GNOME Terminal, macOS Terminal, and Windows Command Prompt.
- **Shell**: The shell is a command interpreter that executes user commands. Common shells include:
  - **Bash**: Bourne Again Shell, widely used in Linux/Unix.
  - **Zsh**: Extended features and user-friendly.
  - **Fish**: User-friendly and interactive.
  
  **Basic Commands**:
  ```bash
  echo "Hello, World!"  # Outputs "Hello, World!"
  pwd  # Prints the working directory
  ```

### **Ch 2. Filesystems**
- **Hierarchy**: Linux/Unix uses a hierarchical filesystem starting with the root `/`.
  - **`/home`**: User directories.
  - **`/bin`**: Essential binaries.
  - **`/etc`**: Configuration files.
  - **`/var`**: Variable data files like logs.

  **File Operations**:
  ```bash
  ls  # Lists files in the directory
  cd /path/to/directory  # Changes the directory
  mkdir new_folder  # Creates a new directory
  touch file.txt  # Creates an empty file
  rm file.txt  # Deletes a file
  ```

### **Ch 3. Permissions**
- **File Permissions**: In Unix-like systems, every file and directory has permissions for the owner, group, and others. The permissions are represented by `r` (read), `w` (write), and `x` (execute).
  
  **Check Permissions**:
  ```bash
  ls -l file.txt  # Lists file with permissions
  ```
  
  **Change Permissions**:
  ```bash
  chmod 755 file.txt  # Sets read, write, execute for owner; read, execute for others
  chmod +x script.sh  # Adds execute permission
  ```

### **Ch 4. Programs**
- **Running Programs**: Execute scripts or binaries directly from the terminal.
  ```bash
  ./script.sh  # Runs the script with the current shell
  python3 script.py  # Runs a Python script
  ```
  
- **Background Processes**:
  ```bash
  ./long_running_task.sh &  # Runs a program in the background
  jobs  # Lists background jobs
  fg %1  # Brings job 1 to the foreground
  ```

### **Ch 5. Packages**
- **Package Managers**: Software tools to install, update, and manage software packages.
  - **`apt`**: Advanced Package Tool for Debian-based systems (e.g., Ubuntu).
  - **`yum`**: Package manager for Red Hat-based systems.
  - **`brew`**: Package manager for macOS.
  
  **Examples**:
  ```bash
  sudo apt update  # Updates package lists
  sudo apt install vim  # Installs the Vim editor
  brew install git  # Installs Git on macOS
  ```
  

# Linux-HandNotes

## Linux Commands and Options

There are 300+ flavors of Linux:
```
Kali Linux: Majority ethical hacking ppl will use this Flavor
Corporate: RedHat, CentOS, Ubuntu, Fedora, IBM AIX, HP_Unix, Cisco Unix, OEL.
```

What we use in lab is RHEL9

## Linux Command Standard Syntax

Command-name {options} {inputs}

```
Options:
  - <Single-Character>
  -- <Single-Word>

Standard Option to all commands is --help
  Ex: uname --help
```

## Command Line Syntaxes

```
$ command -options
```

## Commands

In terminal, the first argument we give to execute is a command.

For example:

```
uname
```

uname is a command and that is the first word of a command line syntax.

## Options

Certain commands are going to have options. Options in Linux Command line are typically a second argument. Usually those options are seen in three formats:

```
<command> -<single character> (Ex: -h , -v )
<command> --<single word> (Ex: --help , --version)
<command> -<single word> (Ex: -version, -help)
```

For example:

```
uname -a
uname --all
```

## Inputs

Certain commands require inputs. Inputs are given with options in some commands and without options for some commands.

For example:

```
ls stands for list
  $ ls /boot
  $ ls -d /boot
```

In the above example, ls is a command, -d is an option, and /boot is an input. The command behavior changes based on whether you use an option or not.

## Hardware and Operating System Information

In general, when we purchase new hardware like laptops or desktops, we look into the configuration of the machine. Let us do the same for the server. This is minimum knowledge required when working on any machine, whether desktop or server.

When you login to the server, run the following commands to see system details. In Linux, everything is a file. You can learn the properties by reading the respective files.

### Check the Vendor of the Operating System

```
$ cat /etc/*release
```

### Check the CPU Information

```
$ cat /proc/cpuinfo
```

### Check the Memory Information

```
$ cat /proc/meminfo
```

### Check the Disk Information

```
$ fdisk -l
$ lsblk
```

### Check the Architecture (32bit or 64bit)

```
$ uname -i

32 bit  -> i386/i586/i686
64 bit  -> x86_64

Note: Starting CentOS 7, operating systems only come in 64 bit. Hence, we always see x86_64.
With this information in hand you will have an idea of the Linux machine you're dealing with and its specifications.
```



## Listing Files and Directories

### List Files

In Windows OS, you generally see the list of files when you open a folder. But Linux is mostly command line, so you may not see files by default. You need to execute a command to check the list of files.

`ls` is a Linux shell command that lists directory contents of files and directories. Some practical examples of ls command are shown below.

```
Syntax: ls <Options> <Path>
```

Note that the ls command works without input (both options and path are optional). It works with or without them.

```
$ ls -ld /opt
```

Get a list of files and directories (may not show hidden files):

```
$ ls
```

Get a list of hidden files and directories:

```
$ ls -A
```

Get a list of files with long format (shows properties of a file):

```
$ ls -l
```

Combine multiple options:

```
$ ls -Al
```

## Note

Giving multiple options depends on the command. ls accepts multiple options but it isn't applicable for all.

### Creating Files

We can create files in multiple ways using different commands in Linux. We will use the `touch` command to create files.

```
Syntax: $ touch <filename>
```

The touch command by default creates an empty file.

```
$ touch file.txt
```

To check the file created:

```
$ ls -l
```

In the above ls command output, you can see the file is an empty file by referring to the fifth column.

The touch command can create multiple files at a single go:

```
$ touch sample notes.txt lambda.py
```

To check the files created:

```
$ ls -l
```

### Important Takeaways

In Linux OS, there are no file extensions. Extensions are given only for user understanding. Also, Linux commands and files are case-sensitive.

```
training.txt and Training.txt are 2 different files (Linux is case-sensitive)
```

### Removing Files

In Linux, we use the `rm` command to remove files. We can also use the `unlink` command which does the same thing, but rm is more widely preferred.

```
Syntax: rm <filename>
```

Example:

```
$ rm fileName.txt
```

Now when you list the files using the ls command, the file should be gone.

```
$ ls
$ rm -i fileName.txt
```

This may ask you for a prompt (yes/no) to remove the file. You can suppress the prompt by adding the -f option:

```
$ rm -f fileName.txt
$ ls
```

**Note:** Be careful while removing a file as it deletes all contents and retrieving lost data is not possible in most cases.

Things you can explore:
- How to remove multiple files?

```
$ rm file1 file2
```

### Copying Files

In Linux, we use the `cp` command to copy files. Alternatively, we have rsync, but cp is more commonly used.

```
Syntax: cp <source-file> <destination-file>
```

Example:

```
$ cp notes.txt pages.txt
```

You can check if the file has been copied by using the ls command:

```
$ ls
```

**Note:** If the destination exists, it will overwrite the file. In some cases, it will ask for a prompt (yes/no) to confirm the overwrite.


## Rename Files

### Renaming/Moving a File

In Linux, to change the name of a file we use the `mv` command.

```
Syntax: mv <source-file> <destination-file>
```

Example:

```
$ mv notes.txt note.txt
```

You can check if the file has been renamed by using the ls command:

```
$ ls
```

**Note:** Unlike Windows, Linux filesystems are case-sensitive. This means that note.txt and NOTE.txt are two different files. Windows FAT and NTFS filesystems are case-insensitive, so note.txt and NOTE.txt would be the same file.

Example:

```
$ mv note.txt NOTE.txt
$ ls
```

**Note:**
- If the destination exists, it will overwrite the file. In some cases, it will ask for a prompt (yes/no) to confirm the overwrite.
- The mv command is intended to move files from one location to another, but we also use it to rename files.

## Creating Directories

### Linux Directory Structure

Unlike any other operating system, Linux also has its own directory structure that starts with `/`.

Reference: [Linux Directory Structure](https://qph.cf2.quoracdn.net/main-qimg-849caf34b204bb41bcb94b20335cab6f)

### Directories

- `/` - Root Directory

Types of files:

```
d - Directory
- - Regular file
l - Link
b - Block devices
c - Character files
S - Socket files
p - Named pipe file
```

### pwd: Present Working Directory

To check which directory you are currently in:

```
$ pwd
```

### General Directory Switch Commands

```
Change from one directory to another:
  $ cd <directory>

  $ cd         # Takes you to home directory
  $ cd -       # Takes you to previous directory
  $ cd ..      # Takes you to parent directory
```

### Directory Sandbox

Create a directory:

```
$ mkdir demo
```

Remove a directory:

```
$ rm -r dirname      # Recursive delete
$ rmdir dirname      # Empty directory only
```

Copy a directory:

```
$ cp -r dir1 dir2
```

Renaming/Moving a directory:

```
$ mv source destination

- If destination does not exist: Rename the directory
- If destination exists:
  - Destination is a file: Invalid operation
  - Destination is a directory: File/Directory will move inside that directory
```

### Basic Connection

In Windows, we use `\` (backslash) to give the path of a file or directory, but in Unix & Linux we use `/` (forward slash).

In Linux, we have a **ROOT DIRECTORY** where the path of any directory ends. A simple forward slash `(/)` is called the **ROOT DIRECTORY**.

There are many directories under `/`, and each has some purpose in the operating system. Unlike Windows, Linux is command-line based, so we use commands to move from one directory to another.

## Navigate Directories

### Present Working Directory

To check your current location in the system:

```
$ pwd
```

### Navigate to Directories

To change the working directory from one location to another, we use the `cd` command.

```
Syntax: cd <directory>
```

Example:

```
$ cd /bin
```

You will switch to the /bin directory.

```
$ pwd
```

You can check your current working directory using the pwd command.

```
$ cd
```

Simple `cd` command will take you to the home directory of the user.

```
$ pwd
```

Observe the output.

```
$ cd -
```

This command will take you to the previous directory that you were using.

### Double Dot (..)

```
$ cd /etc/yum
$ cd ..
$ pwd
$ cd ..
$ pwd
```

`..` means parent directory and takes you to the parent directory of the current directory.

### Single Dot (.)

Dot in Linux indicates the present working directory. You can use it in the commands we have used so far.

```
$ ls

# We will try cp command with the . option
$ cp /etc/passwd .
$ ls
```

Now if you compare the output from the previous ls, you will be able to see the file with name passwd in the present directory.

### User Management

```
# Create a user account named userName
$ sudo useradd userName
$ cat /etc/group

# Create a group account named groupName
$ sudo groupadd groupname

# Add User to the Group
$ sudo usermod -a -G groupName userName

# Change the user password
$ sudo passwd userName

# Delete the user 'userName' from the group 'groupName'
$ sudo gpasswd -d userName groupName
```

## Common Filtering Patterns with awk and cut

```
awk and cut are very powerful file filtering tools on Linux
```

- `cat` - Read the file from top to bottom
- `tac` - Read the file from bottom to top
- `tail` - Read the lines from bottom to top based on the number of mentioned lines (by default, prints the last 10 lines)
- `head` - Read the lines from top to bottom based on the number of mentioned lines (by default, prints the top 10 lines)

### Common Examples of head, tail, cat, tac, sed and cut

```
# cat /etc/passwd                 # Read a file
# cat -n /etc/passwd              # Read and place serial number at start of every line
# tac /etc/passwd                 # Read the file from bottom to top

# head passwd                      # Read top 10 lines
# head -n 5 passwd                # Read first 5 lines

# tail passwd                     # Read last 10 lines
# tail -5 passwd                  # Read last 5 lines
```

### Print Lines from Specific Range

To print lines in between 10 to 15:

```
# sed -n -e '10,14 p' passwd          # Print lines 10 to 14
# sed -n -e '1 p' -e '10 p' passwd    # Print 1st and 10th line
# sed -n -e '9 p' /etc/passwd         # Print specific line

# cat /etc/passwd | grep login        # Find the word "login"
```

### Display First Field in Each Line

To see the first field in every line of the file with a common delimiter:

```
# cut -d : -f1 /etc/passwd           # Display first field

# If you want first and 4th field:
# cut -d : -f1,4 /etc/passwd

# Print fields from 1 to 4:
# cut -d : -f1-4 /etc/passwd
```

![Linux Directory Structure](https://github.com/b54-clouddevops/Linux-Notes/assets/57979895/a3474b34-730f-4212-983a-36710a0208c1)

## Create Directories

Creating a directory is the same as creating a folder in Windows. You can create a directory using the `mkdir` command.

```
$ mkdir demo
```

This will create a new directory named demo. You can check using the ls command:

```
$ ls
```

Now you can see the demo directory listed. To determine if demo is a directory, always use the `ls -l` command output. Directories start with the `d` character.

```
$ mkdir -p demo/new/item1
```

The `-p` option is used to create the directory recursively even if the parent directory is missing.

Create multiple directories:

```
$ mkdir demo1 demo2 demo3 demo4
$ ls
```

### Ownerships

`chown` is the command to change the ownership of files and directories.

```
Syntax: chown userName:groupName fileName.txt
```

Examples:

```
# chown centos:devops fileName.txt           # Change owner & group of file
# chown -r centos:devops dirName/            # Change owner & group of directory
# chown -rf centos:devops dirName/           # Recursively change owner & group
```

### Permissions

In Linux, permissions are classified as:
- Read (`r`) - value 4
- Write (`w`) - value 2
- Execute (`x`) - value 1

```
Syntax: chmod 761 fileName
```

Where:
- 7 = User (Owner)
- 6 = Group
- 1 = Others

```
U: 4+2+1 = 7  # Owner can read, write, and execute
G: 4+2   = 6  # Group can read and write
O: 1     = 1  # Others can just execute
```

### Additional Things to Learn

- There are seven types of files in Linux. Explore each of them.
- Directory and regular file are two of them.
- Types: Directory, Regular File, Block Special File, Character Special File, Named Pipe File, Link File, Socket File.

## Copy Directories

Copying directories uses the same `cp` command that is used to copy files. However, when copying directories, we need to add the `-r` option.

```
Syntax: cp -r dir1 dir2
```

This copies all contents of dir1 into dir2.

**Note:** If dir2 already exists, dir1 will be copied inside dir2.

```
$ cp -r demo1 demo2
```

Copy behavior depends on Target Directory:

```
$ cp SOURCE TARGET

- If TARGET exists and is a file: Invalid operation
- If TARGET exists and is a directory: Copy the file inside the directory
- If TARGET doesn't exist: Copy the directory
```

## Moving/Renaming Directories

### Moving Directories

Moving or renaming directories can be done using the `mv` command.

```
Syntax: mv source destination
```

- If destination doesn't exist: Renames the directory
- If destination exists: Moves the source into the directory

```
$ mv demo4 DEMO4
```

This will rename demo4 to DEMO4.

```
$ ls
```

## Removing Directories

To remove a directory, we use the `rmdir` command in Linux. Removing directories also deletes all files that the directory contains.

```
Syntax: rmdir <directory>
```

Example:

```
$ mkdir demo1
$ ls
$ rmdir demo1
$ ls
```

Check the output to see if the directory was deleted.

In the following example, you will see an error saying the directory is not empty. This is because we have already created sub-directories inside demo.

```
$ mkdir -p demo1/{new,test}
$ rmdir demo1
```

To delete them recursively, we use the `-r` option:

```
$ rm -r demo1
$ ls
```

Sometimes you might be prompted (yes/no) to delete files. If we want a forceful delete without prompting, we use the `-f` option:

```
$ rm -rf demo1
```

**Note:** Once files are removed, there is no way of retrieving them back.


## Concatenate Files

### Concatenate File Content

The `cat` (concatenate) command is very frequently used in Linux. It reads data from files and gives their content as output. It helps us to create, view, and concatenate files.

```
Syntax: cat <filename>
```

Example:

```
$ cat /etc/passwd
```

Show the content of the file.

```
$ cat -n /etc/passwd
```

Show content with line numbers.

```
$ tac /etc/passwd
```

Display the content of the file in reverse order.

Additional things to learn:
- `-A` option in cat command

## Filter Commands

In many situations, you might want only a certain number of lines from a file. You can use filter commands or a combination of them to get your work done.

Filters are typically based on:
- Line Numbers
- Row Filters
- Column Filters

### Head Command

To filter output based on line numbers from the start of the file, use the `head` command.

```
Syntax: head <filename>
```

By default, head command gives you the top 10 lines, but you can change it:

```
$ head /etc/passwd
$ head -n 5 /etc/passwd
```

The second command gives the first 5 lines.

### Tail Command

While head gives you the top lines, `tail` command prints the last lines.

```
Syntax: tail <filename>
```

Tail command will print the last 10 lines by default, but you can change it using the `-n` option:

```
$ tail /etc/passwd
$ tail -n 5 /etc/passwd
```

The second command gives the last 5 lines.

### Grep Command

The `grep` filter searches a file for a particular pattern of characters and displays all lines that contain that pattern. The pattern searched is referred to as a regular expression (grep stands for "globally search for regular expression and print out").

```
Syntax: grep <word> <filename>
```

Example:

```
$ grep root /etc/passwd
```

This fetches all lines which contain the word "root".

### Awk Command

When content needs to be filtered based on columns, we use the `awk` command.

```
Syntax: awk -F 'delimiter' '{print $column-number}' <filename>
```

Examples:

```
$ awk -F : '{print $1}' /etc/passwd
```

This prints the first column.

```
$ awk -F : '{print $1,$2}' /etc/passwd
```

This prints the first and second columns.

Additional things to learn:
- More advanced awk usage patterns

### Cut Command

`cut` helps extract sections of lines based on delimiters.

```
Syntax: cut -d <delimiter> -f <field-number> <filename>
```

Examples:

```
$ cut -d : -f1 /etc/passwd       # Print 1st field
$ cut -d : -f1,4 /etc/passwd     # Print 1st and 4th fields
$ cut -d : -f1-4 /etc/passwd     # Print fields 1-4
```

## Process Management

The most useful commands to see running processes and their utilization are:

```
$ ps
$ top
```

### Examples

```
$ ps -ef                   # Show every process using standard syntax
$ ps -aux                  # Show every process using BSD syntax
$ top                      # Dynamic view, refreshes every 3 seconds
$ ps -U root -u root u     # Every process running as root (real & effective ID)
```

### Kill Command

The `kill` command can terminate any process and its parent process. It has many signals available:

```
Syntax:
  $ kill pID
  $ kill -9 pID      # Forcefully delete a process
```

## Regular Expressions

Resource: [Regular Expressions](https://www.grymoire.com/Unix/Regular.html#uh-6)

### SED & AWK

Resource: [SED & AWK 101 Hacks](https://github.com/chiranjibKonwar/Documentation/blob/master/Sed%20%26%20awk%20101Hacks%20%20.pdf)

## VI Editor

### Linux Editors

There are many editors in different Linux Operating Systems: vi, vim, nano, gedit, emacs, and more. About 90% of operating systems come with vi editor as default.

`vi` is a very powerful editor with many enhanced options in vim. Therefore, we choose to work with vim in our sessions.

### VIM Editor

Vim editor has three modes, each with its own purpose:

1. **ESC Mode** - Perform operations on existing content
2. **COLON Mode** - File and search operations
3. **INSERT Mode** - Add new content

### ESC Mode Operations

#### Line Operations

**Copy Lines:**

```
1. Ensure you are in ESC Mode by pressing ESC
2. Take the cursor to that line
3. Press yy to copy the line
```

**Paste Lines:**

```
1. Take the cursor to the line where you want to paste
2. Press p after performing copy using yy
```

**Delete/Cut Lines:**

```
1. Ensure you are in ESC Mode by pressing ESC
2. Take the cursor to that line
3. Press dd to cut/delete the line
```

#### Word Operations

- Copy words: `yw`
- Paste words: `p`
- Delete words: `dw`

**Note:** Numbers can be combined with any option. For example:
- `10yy` - copy 10 lines
- `5dd` - delete 5 lines
- `u` - undo operations (like Ctrl+Z in Windows)

### COLON Mode Operations

#### Search Operation

```
1. Ensure you are in ESC mode
2. Press : to go to COLON Mode
3. Type :/WORD to search for that word
```

#### Search & Replace

```
1. Ensure you are in ESC mode
2. Press : to go to COLON Mode
3. :%s/WORD1/WORD2/              # Replace first occurrence on each line
4. :%s/WORD1/WORD2/g             # Replace all occurrences (global)
5. :%s/WORD1/WORD2/i             # Case-insensitive replace
```

#### File Operations

- Save file: `:w`
- Quit editor: `:q`
- Quit without saving: `:q!`
- Save and quit: `:wq`

### INSERT Mode

INSERT mode is used to add your own content, whereas the above two modes deal with existing content in the file.

**Note:** There are many more operations available, but we focus on what is needed from a DevOps perspective.

## Find Files

### Finding Files

When you login, you often have no idea where files are located. Since Linux doesn't have a UI, traversing all directories manually would be tedious. The `find` command helps search for files.

```
Syntax: find <location-to-find> <search-criteria>
```

Example:

```
$ find / -name passwd
```

This searches through all directories (starting from `/`). You can narrow down the search by providing a specific directory:

```
$ find /etc -name passwd
```

This only searches in the /etc directory, resulting in fewer results.

Additional resources: [find examples](https://alvinalexander.com/unix/edu/examples/find.shtml)

## Internet Utilities

### Command Line Browser

Often you need to browse URLs and fetch content from the command line. The `curl` command is available to browse content online.

```
Syntax: curl <url>
```

Example:

```
$ curl www.google.com
```

Using curl, we can download files:

```
$ curl https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.0-RC1/bin/apache-tomcat-8.0.0-RC1-deployer.tar.gz -o apache-tomcat-8.0.0-RC1-deployer.tar.gz
```

This downloads the file with the specified filename. Without specifying a filename, it uses the default:

```
$ curl -O https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.0-RC1/bin/apache-tomcat-8.0.0-RC1-deployer.tar.gz
```

## Download Files

Often you need to download software or tools from the internet. The `wget` command downloads files from the internet.

```
Syntax: wget <url>
```

Example (downloading Tomcat):

```
$ wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.0-RC1/bin/apache-tomcat-8.0.0-RC1-deployer.tar.gz
$ ls
```

**Note:** wget doesn't come by default with the OS. You need to install it explicitly. It's better to use curl all the time.

### Extracting Files from tar

Many software packages in the Linux world are packaged in `.zip` or `.tar` format. To extract files from `.tar` extension, use the `tar` command.

```
Syntax: tar -xf <filename>.tar.gz
```

Example:

```
$ tar -xf apache-tomcat-8.0.0-RC1-deployer.tar.gz
```

Where:
- `-x` = extract option
- `-f` = file option

## Pipes

### Pipes

Pipes send the output of one command to another command without storing content on disk.

```
Syntax: com1 | com2
```

Example:

```
$ cat /etc/passwd | grep root
```

**Note:** Not all commands accept inputs via pipes. If we need to take the input, we use the `xargs` command.

Example:

```
$ touch sample.txt
$ ls
$ echo sample.txt | rm -f
$ ls
```

Now use xargs:

```
$ echo sample.txt | xargs rm -f
$ ls
```

## sudo Command

The `sudo` command in Linux gives temporary privileged access to users.

Below commands show how to switch between users:

```
$ sudo su -      # Switch to root user
# whoami         # Shows output as root
```

### How to Give Users sudo Permission

By default in CentOS, apart from root and the centos user, none of the users have root access. The sudoers file determines who has sudo access:

```
$ cat /etc/sudoers   # See the list of users with sudo access
```

## Package Management

In CentOS Linux, packages can be installed in these ways:

1. **dnf** - Package manager (handles dependencies)
2. **rpm** - RPM Package Manager (manual dependency management)
3. **Source Code Based Installation** - [Reference](https://www.makeuseof.com/compile-install-software-from-source-linux/)

### dnf Usage Examples

```
# dnf install packageName -y              # Install package
# dnf remove packageName                  # Delete package
# dnf update packageName                  # Update package
# dnf list installed                      # Show installed packages
# dnf list available                      # Show available packages
# sudo dnf list all                       # Show all packages
# dnf update wget -y                      # Update specific package
# dnf update -y                           # Update all packages
# dnf update --security                   # Update only security packages
# dnf update releasever=9 --security      # Update security packages for specific release
# dnf update releasever=9 --security --exclude=java*  # Exclude certain packages
# rpm -qa | grep packageName              # Check if package is installed
# dnf update `cat package.txt`            # Update packages from file
# dnf info history                        # Check package installation status
# dnf history                             # List all dnf commands executed
```

### rpm Usage Examples

```
# rpm -i packageName.rpm       # Install package
# rpm -U packageName.rpm       # Upgrade package
# rpm -e packageName.rpm       # Delete package
# rpm -q packageName.rpm       # Query package
```

### Repository Configuration

How does dnf know where to download packages? It refers to repos in `/etc/yum.repos.d/*.repo` files.

Example:

```
$ sudo dnf list | grep jenkins -y
```

This command will fail if jenkins isn't available. Let's download a repo file:

```
# Check repos in the system
$ ls /etc/yum.repos.d

# Download Jenkins repo
$ curl https://pkg.jenkins.io/redhat-stable/jenkins.repo -o /etc/yum.repos.d/jenkins.repo

# Check repos now
$ ls /etc/yum.repos.d

# Now install Jenkins
$ sudo dnf list | grep jenkins -y
```

You can also install a package directly from a URL:

```
$ sudo dnf install https://pkg.jenkins.io/redhat-stable/jenkins-2.190.2-1.1.noarch.rpm -y
```

## Service Management

`systemctl` is the command to start, stop, restart, and enable services in CentOS.

### systemctl Usage Examples

```
# systemctl start serviceName
# systemctl stop serviceName
# systemctl restart serviceName
# systemctl enable serviceName
```

## Network Management

```
# curl ifconfig.co            # Show public IP address
# ip -a                       # Show private IP address
# netstat                     # Show network statistics
# netstat -ln                 # Show core network information
# netstat -tulpn              # Show listening ports and associated processes
```

## Filters

### See Complete File Content

```
$ cp /etc/passwd .
$ cat passwd
$ cat -n passwd
$ tac passwd
```

Where:
- `head` - Prints top 10 lines by default
- `tail` - Prints last 10 lines by default

#### Print from End of File

```
$ tail passwd              # Print last 10 lines
$ tail -3 passwd           # Print last 3 lines
```

## cut, sed, awk: Advanced Filtering Tools on Linux

```
# Search and print lines containing a word
Syntax: grep word file
  $ grep ec2-user passwd

# Column-based filtering
Syntax: cut -d <delimiter> -f <number> <file>
  $ cut -d : -f 1 passwd
  $ cut -d : -f 1,5 passwd
  $ cut -d : -f 1-5 passwd
```

## Editors

There are many fancy editors in Linux: vi, vim, nano are few famous editors to edit files. They are essentially notepads.

```
vim editor is not available by default in CentOS 7 and needs to be installed:
  $ sudo yum install vim -y

Usage example:
  $ vim filename.txt
```

### vim Modes

```
1. ESC Mode
2. COLON Mode
3. INSERT Mode

To edit a file:
  $ vim filename

To enter content:
  - Press i to enter INSERT Mode
  - Type your content
  - Press ESC to return to ESC Mode
  - Type :wq! to save and exit

Legend:
  w = Write
  q = Quit
  ! = End of expression

Search content using forward slash /:
  Use the forward slash / to search within the editor.
```

### VIM Search and Replace Examples

```
%s/word1/word2/     - Replace first occurrence on each line
%s/word1/word2/g    - Replace all occurrences on each line (global)
s/word1/word2/      - Replace first occurrence on current line
s/word1/word2/g     - Replace all occurrences on current line
```

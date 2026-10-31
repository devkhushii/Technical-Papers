# Linux CLI – Quick Revision Cheat Sheet

## 1. Navigation

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls` | List files and directories |
| `cd folder` | Move into a directory |
| `cd ..` | Move one directory up |
| `cd ~` | Go to home directory |
| `cd -` | Go to previous directory |
| `cd /` | Go to root directory |
| `tree` | Display directory structure |

**Important `ls` flags:**

```bash
ls -l       # Detailed list
ls -a       # Include hidden files
ls -h       # Human-readable file sizes
ls -t       # Sort by modification time
ls -r       # Reverse order
ls -lahtr   # Detailed, hidden, human-readable, oldest first
```

## 2. File and Directory Management

| Command | Purpose |
|---|---|
| `mkdir folder` | Create directory |
| `mkdir -p a/b/c` | Create nested directories |
| `touch file.txt` | Create an empty file |
| `cp a.txt b.txt` | Copy a file |
| `cp -r dir1 dir2` | Copy directory recursively |
| `mv a.txt folder/` | Move a file |
| `mv old.txt new.txt` | Rename a file |
| `rm file.txt` | Delete a file |
| `rm -r folder` | Delete directory and its contents |
| `rmdir folder` | Delete an empty directory |

## 3. Reading and Editing Files

| Command | Purpose |
|---|---|
| `cat file.txt` | Display file content |
| `less file.txt` | Read file page by page |
| `head file.txt` | Show first 10 lines |
| `head -n 3 file.txt` | Show first 3 lines |
| `tail file.txt` | Show last 10 lines |
| `tail -n 30 file.txt` | Show last 30 lines |
| `tail -f app.log` | Watch new log entries |
| `nano file.txt` | Edit a file |
| `vim file.txt` | Open file in Vim |

## 4. Searching and Counting

| Command | Purpose |
|---|---|
| `find . -name "*.py"` | Find Python files |
| `find ~ -iname "*java*"` | Find names containing Java |
| `grep "error" file.txt` | Search text in a file |
| `grep -i "error" file.txt` | Case-insensitive search |
| `grep -n "error" file.txt` | Show matching line numbers |
| `grep -r "error" .` | Search recursively |
| `wc -l file.txt` | Count lines |
| `wc -w file.txt` | Count words |
| `wc -c file.txt` | Count bytes |

**Important `grep` flags:**
- `-i` — Ignore case.
- `-n` — Show line numbers.
- `-r` — Search recursively.
- `-w` — Match whole words.
- `-o` — Print only matched text.

```bash
grep -ow "Harry" book.txt | wc -l
```

## 5. Pipes and Text Processing

| Command | Purpose |
|---|---|
| `command1 \| command2` | Pass output to another command |
| `>` | Redirect output and overwrite file |
| `>>` | Append output to file |
| `sort file.txt` | Sort lines |
| `sort file.txt \| uniq` | Remove consecutive duplicate lines |
| `awk '{print $1}' file.txt` | Print first column |
| `sed 's/old/new/g' file.txt` | Replace text |
| `xargs` | Pass input as command arguments |

**Examples:**

```bash
ps aux | grep firefox
```

```bash
cat names.txt | sort | uniq
```

```bash
echo "Hello" > file.txt
echo "World" >> file.txt
```

## 6. File Permissions and Ownership

```bash
ls -l
chmod 755 file.txt
chmod -R 755 folder/
chown user file.txt
sudo chown user:group file.txt
```

**Permission numbers:**

| Number | Permission |
|---|---|
| `4` | Read (r) |
| `2` | Write (w) |
| `1` | Execute (x) |
| `7` | Read + Write + Execute |
| `5` | Read + Execute |
| `6` | Read + Write |

Example: `chmod 755 file.txt`

- Owner: `7` = rwx
- Group: `5` = r-x
- Others: `5` = r-x

**Important flags:**
- `-R` — Apply changes recursively to all files and subdirectories.

## 7. Process Management

| Command | Purpose |
|---|---|
| `ps` | Show processes |
| `ps aux` | Show all running processes |
| `ps -ef` | Detailed process list |
| `ps -p PID` | Show a specific process |
| `top` | Monitor running processes |
| `htop` | Interactive process monitor |
| `pgrep firefox` | Find process ID by name |
| `kill PID` | Terminate a process |
| `kill -9 PID` | Forcefully terminate a process |
| `kill -STOP PID` | Pause a process |
| `kill -CONT PID` | Resume a process |

**Find PID and PPID:**

```bash
ps -o pid,ppid,cmd -p PID
```

- `PID` — Process ID.
- `PPID` — Parent Process ID.

**Find and terminate a process using a pipe:**

```bash
ps aux | grep firefox
ps aux | grep firefox | awk '{print $2}' | xargs kill
```

**Important flags:**
- `-o` — Select columns to display.
- `-p` — Specify process ID.
- `-9` — Force kill.

## 8. System Information and Disk Usage

| Command | Purpose |
|---|---|
| `df -h` | Show disk space |
| `du -sh folder/` | Show folder size |
| `free -h` | Show memory usage |
| `uname -a` | Show system information |
| `uname -m` | Show machine architecture |
| `date` | Show current date and time |
| `whoami` | Show current username |
| `groups` | Show user's groups |
| `lspci` | List PCI devices |
| `printenv` | Show environment variables |
| `echo $SHELL` | Show current shell |

## 9. Networking

| Command | Purpose |
|---|---|
| `ping google.com` | Check network connectivity |
| `host google.com` | Find domain IP addresses |
| `ip addr` | Show IP addresses |
| `ss -tunap` | Show network connections and processes |
| `ss -tuln` | Show listening TCP/UDP ports |
| `ss -tulnp` | Show listening ports with process details |
| `ssh user@host` | Connect to a remote machine |

**Find process using a particular port:**

```bash
sudo ss -tulnp | grep :5432
```

## 10. Package Management (Ubuntu)

| Command | Purpose |
|---|---|
| `sudo apt update` | Update package information |
| `sudo apt upgrade` | Upgrade installed packages |
| `sudo apt install htop` | Install a package |
| `sudo apt remove nginx` | Uninstall a package |
| `sudo apt autoremove` | Remove unused dependencies |

## 11. Other Useful Commands

| Command | Purpose |
|---|---|
| `man command` | Open command manual |
| `history` | Show previously executed commands |
| `which python` | Show command location |
| `whereis python` | Locate binary and related files |
| `wget URL` | Download a file |
| `rsync -av source/ destination/` | Synchronize files and directories |

## 12. Important Terminal Shortcuts

| Shortcut | Purpose |
|---|---|
| `Ctrl + C` | Stop running command |
| `Ctrl + Z` | Suspend running process |
| `Ctrl + D` | Exit terminal/input |
| `Ctrl + R` | Search command history |
| `Tab` | Auto-complete command or path |
| `↑ / ↓` | Navigate command history |

## 13. Important Linux Directories

| Directory | Purpose |
|---|---|
| `/` | Root directory |
| `/bin` | Essential commands |
| `/sbin` | System administration commands |
| `/etc` | Configuration files |
| `/home` | Users' home directories |
| `/root` | Root user's home directory |
| `/tmp` | Temporary files |
| `/usr` | User applications and utilities |
| `/var` | Logs and frequently changing data |
| `/opt` | Optional software |
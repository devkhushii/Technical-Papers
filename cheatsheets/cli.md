# Linux CLI 

##  Shell Basics

A shell is a program that accepts commands from users and passes them to the operating system for execution.

Bash (Bourne Again Shell) is one of the commonly used Linux shells.

**Check the current shell**
```bash
echo $SHELL          # Display the default login shell
ps -p $$             # Display the currently running shell process
ps -p $$ -o comm=    # Display only the shell name
```

## Navigation Commands

**Check current directory**
```bash
pwd
```

**List files and directories**
```bash
ls
ls -l       # -l: long format (permissions, owner, size, date)
ls -a       # -a: show hidden files and directories
ls -h       # -h: show file sizes in human-readable format
ls -t       # -t: sort by modification time
ls -r       # -r: reverse the sorting order
ls -lahtr   # Combine flags: detailed, hidden, readable sizes, time-sorted, reversed
ls *.txt       # *: matches any number of characters
ls file?.txt   # ?: matches exactly one character
ls .*          # Matches hidden filenames beginning with a dot
```


**Change directory**
```bash
cd folder_name
cd ..       # ..: move one directory up
cd ~        # ~: move to the home directory
cd -        # -: return to the previous directory
```


**Display directory structure**
```bash
tree
tree -L 2   # -L: limit the display to 2 directory levels
```


##  File and Directory Management

**Create a directory**
```bash
mkdir folder_name
mkdir -p parent/child   # -p: create parent directories if they don't exist
```


**Create an empty file**
```bash
touch file.txt
```


**Copy files and directories**
```bash
cp file.txt copy.txt
cp -r folder1 folder2   # -r: copy directories recursively, including contents
```


**Move or rename files**
```bash
mv old.txt new.txt
mv file.txt folder/
```


**Remove files and directories**
```bash
rm file.txt
rm -r folder_name      # -r: remove directories and their contents recursively
rm -i file.txt         # -i: ask for confirmation before removing
```


**Remove an empty directory**
```bash
rmdir folder_name
```


## 3. Reading and Editing Files

**Display file content**
```bash
cat file.txt
```


**Read a file page by page**
```bash
less file.txt
```

Displays file content one screen at a time. Press Space to move forward.
```bash
more file.txt
```

**Display the first lines**
```bash
head file.txt
head -n 5 file.txt   # -n: display the first 5 lines
```


**Display the last lines**
```bash
tail file.txt
tail -n 5 file.txt   # -n: display the last 5 lines
tail -f log.txt      # -f: keep watching the file for new content
```


**Edit a file**
```bash
nano file.txt
vim file.txt
```


## 4. Searching and Counting

**Find files and directories**
```bash
find . -name "file.txt"       # -name: search by exact filename pattern
find . -type f                # -type f: search only for files
find . -type d                # -type d: search only for directories
find . -name "*.py"           # *.py: find files ending with .py
find ~ iname '*java*'         # Searches the home directory for filenames containing java. -iname makes the search case-insensitive.
```


**Search for text inside files**
```bash
grep "hello" file.txt
grep -i "hello" file.txt      # -i: ignore uppercase/lowercase differences
grep -n "hello" file.txt      # -n: display matching line numbers
grep -r "hello" folder/       # -r: search inside files in a directory recursively
grep -w "hello" file.txt      # -w: match the complete word only
grep -o "hello" file.txt      # -o: display only the matching text
```


**Count lines, words and characters**
```bash
wc file.txt
wc -l file.txt    # -l: count lines
wc -w file.txt    # -w: count words
wc -c file.txt    # -c: count bytes
```


**Count occurrences of a word**
```bash
grep -iow "Harry" book.txt | wc -l
```


## 5. Pipes and Text Processing

**Pipe operator**  : Sends the output of one command as input to another command.
```bash
ls | wc -l
```


**Redirect output** : Saves command output into a file.
```bash
ls > output.txt      # >: write output and overwrite existing content
ls >> output.txt     # >>: append output without overwriting existing content
```


**Sort content**
```bash
sort names.txt
sort -r names.txt    # -r: sort in reverse order
sort -n numbers.txt  # -n: sort numerically instead of alphabetically
```


**Remove duplicate adjacent lines**
```bash
uniq names.txt
uniq -c names.txt    # -c: display the count of each repeated line
```


**Extract columns using awk**
```bash
awk '{print $1}' file.txt
awk '{print $2}' file.txt    # $2: display the second column
awk '{print $1, $3}' file.txt
```


**Replace text using sed**
```bash
sed 's/old/new/' file.txt    # replace first occurrence of old with new in each line
sed 's/old/new/g' file.txt   # g: replace all occurrences in each line
```
**Display a Specific Range of Lines**
```bash 
sed -n '100,200p' book.txt   # Displays lines 100 to 200. -n prevents automatic printing, and p prints the selected lines.
```

**Count Unique Words in a File**
```bash
grep -oE '[[:alnum:]]+' book.txt | tr '[:upper:]' '[:lower:]' | sort -u | wc -l
```
- grep -oE: Extracts individual words using a pattern.
- tr: Converts uppercase letters to lowercase.
- sort -u: Sorts words and removes duplicates.
- wc -l: Counts the unique words.

**Pass output as arguments using xargs**
```bash
echo "file1.txt file2.txt" | xargs rm      # Converts input into arguments for another command.
```


**Display formatted output**
```bash
printf "Hello %s\n" "Kanika"
```
Prints formatted text. `\n` adds a new line.

## 6. File Permissions and Ownership

**Check file permissions**
```bash
ls -l
```

**Change permissions**
```bash
chmod 755 script.sh
chmod -R 755 folder/    # -R: apply permissions recursively to contents
```


**Permission numbers**

| Number | Permission | Meaning |
|---|---|---|
| 4 | Read (r) | View content |
| 2 | Write (w) | Modify content |
| 1 | Execute (x) | Run a file or access a directory |
| 7 | rwx | Read, write and execute |
| 6 | rw- | Read and write |
| 5 | r-x | Read and execute |

**Example:**
```bash
chmod 755 script.sh
```
- Owner: `7` = read, write, execute.
- Group: `5` = read, execute.
- Others: `5` = read, execute.

**Change ownership**
```bash
sudo chown user file.txt
sudo chown user:group file.txt
sudo chown -R user:group folder/   # -R: change ownership recursively
```


## 7. Process Management

**Display running processes**
```bash
ps
ps aux   # display all process in detailed format
```


**Display selected process details**
```bash
ps -p 1234                 # -p: select a process using its PID
ps -o pid,ppid,cmd -p 1234 # -o: choose which columns to display
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 4  # Display the top 3 processes by CPU usage
```


**Monitor processes continuously**
```bash
top
htop
```

**Find process IDs**
```bash
pgrep firefox
pgrep -f firefox    # -f: search the complete command line
```
.

**Terminate a process**
```bash
kill 1234
kill -9 1234    # -9: forcefully terminate the process
```


**Stop and continue a process**
```bash
kill -STOP 1234   # -STOP: pause the process
kill -CONT 1234   # -CONT: resume the process
```


## 8. Parent and Child Processes

**Display process hierarchy**
```bash
pstree -p   # Displays processes in a tree structure. `-p` shows process IDs.

```

**Display parent and child process details**
```bash
ps -o pid,ppid,cmd
```
- `PID`: Process ID.
- `PPID`: Parent Process ID.
- `CMD`: Command that started the process.

**Display process ancestry**
```bash
pstree -sp 1234    # `-s` displays the parent process chain, and `-p` displays process IDs.
```

## 9. System and Disk Information

**Check disk space**
```bash
df -h   # `-h` shows sizes in human-readable units.
```
Displays available and used disk space. 

**Check directory size**
```bash
du -sh folder/         # `-s` displays only the total size
```

**Check memory usage** 
Displays RAM and swap memory usage. 
```bash
free -h
```

**Display system information**
Displays detailed operating system and kernel information. `-a` means all available information.
```bash
uname -a
```


**Display current date and time**
```bash
date
```

**Display current username**
```bash
whoami
```

**Display user groups**
```bash
groups
```


**Display hardware information**
```bash
lspci
```


**Display environment variables**
```bash
printenv
echo $SHELL
```


## 10. Networking Commands

**Check network connectivity**
```bash
ping google.com
ping -c 4 google.com    # -c: send only 4 packets
```
**Display network congifguration**
```bash
ifconfig
```

**Look up domain IP addresses**
Finds the IP addresses associated with a domain name.
```bash
host google.com
```


**Display IP addresses**
```bash
ip addr
```

**Check network connections and ports**
```bash
ss -tuln
ss -tulnp
```
- `-t`: show TCP connections.
- `-u`: show UDP connections.
- `-l`: show listening sockets.
- `-n`: show numeric addresses and port numbers.
- `-p`: show the process using the socket (may require `sudo`).

**Check a specific port**
Checks whether a process is listening on port `5432`.
```bash
sudo ss -tulnp | grep :5432
```


**Connect to a remote machine**
```bash
ssh username@server_ip
```


## 11. Ubuntu Package Management

**Update package information**
```bash
sudo apt update
```


**Upgrade installed packages**
```bash
sudo apt upgrade
```


**Install a package**
```bash
sudo apt install package_name
```


**Remove a package**
```bash
sudo apt remove package_name
```


**Remove unused packages**
```bash
sudo apt autoremove
```


## 12. Other Useful Commands

**Display command manual**
```bash
man ls
```

**Display command history**
```bash
history
```


**Find command location**
```bash
which python
```


**Find command information**
```bash
whereis python
```


**Download a file**
```bash
wget https://example.com/file.zip
```

**Start a Python server**
```bash
python3 -m http.server 8000
```

**Copy files between locations**
```bash
rsync -av source/ destination/
```
- `-a`: archive mode; preserves important file properties.
- `-v`: verbose; displays details while copying.



## 13. Terminal Shortcuts

| Shortcut | Use |
|---|---|
| `Ctrl + C` | Stop the running command |
| `Ctrl + Z` | Suspend the running process |
| `Ctrl + D` | Exit the current shell or send EOF |
| `Ctrl + L` | Clear the terminal screen |
| `Ctrl + A` | Move to the beginning of the line |
| `Ctrl + E` | Move to the end of the line |
| `Ctrl + R` | Search command history |
| `Tab` | Auto-complete commands and filenames |
| `↑ / ↓` | Navigate command history |

## 14. Important Linux Directories

| Directory | Purpose |
|---|---|
| `/` | Root directory; starting point of the filesystem |
| `/home` | Contains users' personal directories |
| `/root` | Home directory of the root user |
| `/etc` | Contains system configuration files |
| `/bin` | Contains essential user commands |
| `/usr` | Contains user applications and utilities |
| `/var` | Contains changing data such as logs |
| `/tmp` | Stores temporary files |
| `/dev` | Contains device files |
| `/proc` | Contains process and kernel information |
| `/sbin` | Contains system administration commands. |
| `/opt` | Stores optional or third-party software. |
| `/var/log` | Stores system and application log files. |


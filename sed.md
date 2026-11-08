# Stream Editor (`sed`) in Linux

## 1. Introduction to `sed`

- `sed` stands for **Stream Editor**.
- It is a command-line utility in Linux used to search, filter, replace, insert, append, and delete text.
- It processes input line by line and applies specified operations without opening the file in a text editor.
- By default, `sed` does not modify the original file. It displays the modified output on the terminal.

### Basic Syntax

```bash
sed [OPTIONS] 'COMMAND' filename
```

---

## 2. How `sed` Works

By default, `sed` follows these steps:

1. Reads one line from the input.
2. Stores the line in an internal temporary memory area called **Pattern Space**.
3. Applies the specified commands to that line.
4. Prints the processed line to standard output.
5. Moves to the next line.
6. Repeats the process until the input is exhausted.

---

## 3. Working with Line Addresses

An address tells `sed` which line or lines should be affected by a command.

### Types of Addresses

| Address | Meaning |
|---|---|
| `1` | First line |
| `5` | Fifth line |
| `$` | Last line |
| `1,5` | Lines 1 to 5 |
| `2,$` | Line 2 to the last line |
| `/Linux/` | Lines containing `Linux` |
| `/^Hello/` | Lines starting with `Hello` |
| `/Linux$/` | Lines ending with `Linux` |

### Pattern-Based Address Ranges

We can also select a range using two patterns.

```bash
sed -n '/Hello/,/Java/p' sample.txt
```

Prints from a line matching `Hello` through the next line matching `Java`, including both matching lines. If another `Hello` appears later, `sed` can select another range.

---

## 4. Basic `sed` Operations

### 4.1 Substitute Command (`s`)

The substitute command searches for a particular pattern and replaces it with another string.

**Syntax:**

```bash
sed 's/old_text/new_text/' filename
```

#### Substitute Command Flags

**1. Global Replacement (`g`)**

By default, `sed` replaces only the first occurrence on each line.

```bash
sed 's/Linux/Ubuntu/g' sample.txt
```

The `g` flag replaces all occurrences of the matching text on each line.

**2. Replace a Specific Occurrence**

```bash
sed 's/Linux/Ubuntu/2' sample.txt
```

Replaces only the second occurrence of `Linux` on each line.

**3. Case-Insensitive Replacement (`i`)**

```bash
sed 's/linux/Ubuntu/gi' sample.txt
```

Matches `linux`, `Linux`, and `LINUX` without considering case.

*Note: `i` is a GNU `sed` extension.*

**4. Print Only When Replacement Happens (`p`)**

```bash
sed -n 's/Linux/Ubuntu/gp' sample.txt
```

Prints only those lines where a replacement takes place.

**5. Write Lines Where Replacement Happens (`w`)**

```bash
sed 's/Linux/Ubuntu/gw changes.txt' sample.txt
```

Writes lines where a substitution occurred into `changes.txt`. Normal output is also printed because `-n` is not used.

**6. Multiple Substitutions**

```bash
sed 's/Linux/Ubuntu/g; s/Python/Java/g' sample.txt
```

Performs two replacements in the same command.

### 4.2 Delete Command (`d`)

The delete command removes selected lines from the output.

**Syntax:**

```bash
sed 'ADDRESSd' filename
```

**Examples:**

```bash
sed '1d' sample.txt
```

Deletes the first line.

```bash
sed '2,5d' sample.txt
```

Deletes lines 2 to 5.

```bash
sed '1,$d' sample.txt
```

Deletes all lines from the output.

```bash
sed '/Linux/d' sample.txt
```

Deletes all lines containing `Linux`.

```bash
sed '/^$/d' sample.txt
```

Deletes empty lines.

```bash
sed '/Python/!d' sample.txt
```

Keeps only lines containing `Python`.

### 4.3 Print Command (`p`)

The print command is used to print selected lines.

**Syntax:**

```bash
sed -n 'ADDRESSp' filename
```

**Examples:**

```bash
sed -n '1p' sample.txt
```

Prints only the first line.

```bash
sed -n '3,6p' sample.txt
```

Prints lines 3 to 6.

```bash
sed -n '$p' sample.txt
```

Prints the last line.

```bash
sed -n '/Linux/p' sample.txt
```

Prints lines containing `Linux`.

```bash
sed -n '/^Python/p' sample.txt
```

Prints lines starting with `Python`.

#### What is the purpose of `-n`?

Normally, `sed` automatically prints every processed line.

The `-n` option suppresses automatic printing.

**Without `-n`:**

```bash
sed '2p' sample.txt
```

The second line is printed twice because:
- Automatic printing prints every line.
- The `p` command explicitly prints the second line.

**With `-n`:**

```bash
sed -n '2p' sample.txt
```

Only the second line is printed once.

### 4.4 Insert Command (`i`)

The insert command adds new text before a specified line.

**Syntax:**

```bash
sed 'ADDRESSi\TEXT' filename
```

**Example:**

```bash
sed '2i\This is a new line' sample.txt
```

Inserts the given text before line 2.

### 4.5 Append Command (`a`)

The append command adds new text after a specified line.

**Syntax:**

```bash
sed 'ADDRESSa\TEXT' filename
```

**Examples:**

```bash
sed '2a\This line is appended' sample.txt
```

Adds text after line 2.

```bash
sed '$a\This is the last line' sample.txt
```

Adds text at the end of the file.

### 4.6 Change Command (`c`)

The change command replaces the entire selected line with new text.

**Syntax:**

```bash
sed 'ADDRESSc\NEW_TEXT' filename
```

**Examples:**

```bash
sed '2c\This line has been replaced' sample.txt
```

Replaces line 2 completely.

```bash
sed '/Python/c\This line contains programming information' sample.txt
```

Replaces every line containing `Python` with the specified text.

---

## 5. Regular Expressions in `sed`

Regular expressions (Regex) are patterns used to match text. They allow `sed` to search for patterns instead of only exact words.

### Common Regex Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `^` | Beginning of a line | `^Hello` |
| `$` | End of a line | `Linux$` |
| `.` | Any single character | `L.nux` |
| `*` | Zero or more occurrences of the preceding character | `ab*` |
| `[abc]` | Any one character from the set | `[abc]` |
| `[^abc]` | Any character except those in the set | `[^abc]` |
| `[0-9]` | Any digit | `[0-9]` |
| `[a-z]` | Lowercase letters | `[a-z]` |
| `[A-Z]` | Uppercase letters | `[A-Z]` |
| `\+` | One or more occurrences (GNU BRE extension) | `a\+` |
| `\?` | Zero or one occurrence (GNU BRE extension) | `a\?` |
| `\{n\}` | Exactly `n` occurrences | `a\{3\}` |

### Practical Examples

**1. Lines starting with `Hello`**

```bash
sed -n '/^Hello/p' sample.txt
```

**2. Lines ending with `Linux`**

```bash
sed -n '/Linux$/p' sample.txt
```

**3. Lines containing digits**

```bash
sed -n '/[0-9]/p' sample.txt
```

**4. Delete lines containing digits**

```bash
sed '/[0-9]/d' sample.txt
```

**5. Replace multiple spaces with a single space**

```bash
sed 's/  */ /g' sample.txt
```

**6. Remove leading spaces**

```bash
sed 's/^ *//' sample.txt
```

**7. Remove trailing spaces**

```bash
sed 's/ *$//' sample.txt
```

**8. Remove both leading and trailing spaces**

```bash
sed 's/^ *//; s/ *$//' sample.txt
```

### Basic vs Extended Regular Expressions

By default, `sed` uses Basic Regular Expressions (BRE).

For Extended Regular Expressions (ERE), use the `-E` option.

**Example using BRE:**

```bash
sed -n '/[0-9]\+/p' sample.txt
```

**Example using ERE:**

```bash
sed -E -n '/[0-9]+/p' sample.txt
```

In ERE:
- `+` means one or more occurrences.
- `?` means zero or one occurrence.
- `()` is used for grouping.
- `|` is used for alternatives.

**Example:**

```bash
sed -E 's/(Python|Java)/Programming/g' sample.txt
```

Replaces either `Python` or `Java` with `Programming`.

---

## 6. In-Place Editing (`-i`)

By default, `sed` displays modified output without changing the original file.

To modify the original file directly, use the `-i` option.

**Syntax:**

```bash
sed -i 'COMMAND' filename
```

**Example:**

```bash
sed -i 's/Linux/Ubuntu/g' sample.txt
```

Replaces every occurrence of `Linux` with `Ubuntu` directly in the file.

### Creating a Backup Before Editing

```bash
sed -i.bak 's/Linux/Ubuntu/g' sample.txt
```

This:
1. Creates a backup named `sample.txt.bak`.
2. Modifies the original `sample.txt`.

*Important: `-i` syntax differs between GNU `sed` (commonly used on Linux) and BSD `sed` (commonly used on macOS).*

---

## 7. Other Useful `sed` Commands

**1. Quit after processing the first three lines**

```bash
sed '3q' sample.txt
```

**2. Print line numbers**

```bash
sed -n '=' sample.txt
```

**3. Translate lowercase characters into uppercase**

```bash
sed 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/' sample.txt
```

**4. Print the first three lines and stop**

```bash
sed -n '1,3p; 3q' sample.txt
```

---

## 8. Using `sed` with Pipes

A pipe (`|`) passes the output of one command as the input of another command.

`sed` can be combined with commands such as `cat`, `grep`, `ls`, and `ps`.

### Examples

**1. Using `cat` with `sed`**

```bash
cat sample.txt | sed 's/Linux/Ubuntu/g'
```

Passes the contents of the file to `sed`. For this simple case, `sed 's/Linux/Ubuntu/g' sample.txt` is shorter and does the same thing.

**2. Using `grep` with `sed`**

```bash
grep 'Python' sample.txt | sed 's/Python/Java/g'
```

First filters lines containing `Python` and then replaces `Python` with `Java`.

**3. Using `sed` with `ps`**

```bash
ps aux | sed -n '1,5p'
```

Displays the first five lines of process information.

**4. Using `sed` with `ls`**

```bash
ls -l | sed -n '1,5p'
```

Displays the first five lines of directory listing output.

---

## 9. Practical Real-World Use Cases

### 1. Replacing Configuration Values

```bash
sed -i 's/PORT=8000/PORT=9000/' config.txt
```

Updates the port value in a configuration file.

### 2. Removing Comments from a File

```bash
sed '/^#/d' config.txt
```

Deletes lines beginning with `#`.

### 3. Removing Empty Lines

```bash
sed '/^$/d' sample.txt
```

Removes empty lines.

### 4. Extracting Specific Log Entries

```bash
sed -n '/ERROR/p' application.log
```

Displays lines containing `ERROR`.

### 5. Replacing IP Addresses

```bash
sed 's/192\.168\.1\.1/10.0.0.1/g' config.txt
```

Replaces the specified IP address. The dots are escaped because `.` has a special meaning in regular expressions.

### 6. Adding a Comment to the First Line

```bash
sed '1i\# Configuration File' config.txt
```

Inserts a comment before the first line.

---

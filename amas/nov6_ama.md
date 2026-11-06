# Nov 6, 2026 - AMA

## Are Keys mutatable or not in dictionary?
- Dictionary keys must be immutable (hashable). We can use strings, numbers, and tuples as keys, but we cannot use lists or dictionaries as keys.

## What is the command to check permision in cli?
- we use ` ls -l ` command to list file with permission.

## dictionary predefined functions?
 - Some commonly used dictionary methods are:
```bash
 keys()    # Returns all keys.
 values()   # Returns all values.
 items()   #  Returns key-value pairs.
 get()      # Returns the value of a specified key.
 update()   #  Updates the dictionary.
 pop()    #  Removes a specified key.
 popitem()   #  Removes the last inserted key-value pair.
 clear()   #  Removes all elements.
 copy()   #  Creates a copy of the dictionary.
 setdefault()   # Returns the value of a key or inserts it if it doesn't exist.
```

## What is staging area?
- The staging area in Git is an intermediate area where we prepare changes before committing them.
- We use the git add command to move changes to the staging area.

## What is mutable and immutable?
- Mutable: Objects whose values can be changed after creation.
- Immutable: Objects whose values cannot be changed after creation.

## What is List index start from?
- list index start from 0.

## How do we sort using buillt in in list
- by using `.sort()` and ` sorted()`  function

## how can i get keys in dictionary?
- by using ` .keys()` function.

## What is type casting?
- Type casting is the process of converting one data type into another data type.
```bash 
num = "100"
result = int(num)

print(result)       # 100
print(type(result)) # <class 'int'>
```

## if a two keys are same in a dictionary which value is going to store finally?
- If a dictionary contains duplicate keys, the latest assigned value will overwrite the previous value.

## What is the difference between * and "?"
- **\*** matches zero or more characters.
- **?** matches exactly one character.
## how to get all the directories and file details?
- We use the ls -l command to display detailed information about files and directories.

##  how can we get index and index value?
- We use the enumerate() function to get both the index and value while iterating over a list.

## What is the use of pip?
- pip is Python's package installer. It is used to install, upgrade, and uninstall Python libraries and packages.

## What the service and application?
- Application: A software program designed to perform specific tasks for users. Example: Chrome, VS Code, or a calculator.
- Service: A program or process that runs in the background and provides functionality to other applications or users. Example: SSH service, database service, or web server.

## What is the diff between home and root directory ?
- Home Directory (/home/username):
      - It is the personal directory of a user.
      - It stores personal files, documents, and settings.
    
- Root Directory (/):
      - It is the top-level directory in the Linux file system.
      - All files and directories exist under it.

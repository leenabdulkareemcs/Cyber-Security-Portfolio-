# Lab 08 — Linux CLI Fundamentals

This lab covers practical command-line tasks in Linux:
1) Changing things (creating/moving/copying/deleting files and folders)
2) File permissions (reading and changing permissions with chmod)
3) Editing files (Nano and Vim basics)
4) Using wc (counting lines/words/characters)

---

## 1) Changing Things (Files and Folders)

### Create a directory
```bash
mkdir <directory-name>
````

Example:

```bash
mkdir examplefolder
ls
```

### Create a new empty file

```bash
touch <filename>
```

Example:

```bash
touch newfile.txt
ls
```

### Move or rename files (mv)

Move to parent directory:

```bash
mv myfile ..
```

Rename in the same directory:

```bash
mv oldname.txt newname.txt
```

Move and rename at the same time:

```bash
mv myfile ../newfile
```

### Copy files (cp)

```bash
cp original.txt copy.txt
```

### Delete files and directories (rm)

Delete a file (permanent):

```bash
rm file.txt
```

Delete a directory and all contents (permanent):

```bash
rm -r foldername
```

Notes:

* rm permanently deletes (no recycle bin).
* Use extra caution with rm -r.

---

## 2) File Permissions

### View permissions

```bash
ls -la
```

Permissions format:

* First character: file type

  * d = directory
  * * = regular file
* Next 9 characters: permissions in 3 groups

  * Owner (user)
  * Group
  * Others (world)

Permission letters:

* r = read
* w = write
* x = execute

Example:

```text
drwxr-xr-x
```

### Numeric notation

Each digit represents (r=4, w=2, x=1):

* 7 = rwx
* 6 = rw-
* 5 = r-x
* 4 = r--
* 3 = -wx
* 2 = -w-
* 1 = --x
* 0 = ---

Example: chmod 755

* Owner: 7 (rwx)
* Group: 5 (r-x)
* Others: 5 (r-x)

Result:

```text
rwxr-xr-x
```

### Change permissions with chmod

Numeric:

```bash
chmod 754 myfile
```

Symbolic:
Add execute for all users:

```bash
chmod +x myfile
```

Remove write:

```bash
chmod -w myfile
```

Recursive change for a directory:

```bash
chmod -R 755 /home/linux
```

### Special permissions (identification)

* SUID: shown as s or S in the owner's execute position
* SGID: shown as s or S in the group's execute position
* StickyBit: shown as t or T in the others' execute position

Examples:

```text
-rwSr--r--   (SUID set, owner execute not set)
-rw-r-Sr--   (SGID set, group execute not set)
-rwxr-xr-t   (StickyBit set)
```

World-writable file:

* If Others permissions include w (e.g., ...rw-, ...rwx, ...-wx)

---

## 3) Editing Files (Nano and Vim)

### Create a new file

```bash
touch myfile.txt
```

### Nano

Open:

```bash
nano myfile.txt
```

Common shortcuts:

* Save: Ctrl + O, then Enter
* Exit: Ctrl + X
* Search: Ctrl + W

### Vim

Open:

```bash
vim myfile.txt
```

Core workflow:

* Insert mode: press i
* Return to command mode: press Esc
* Save and quit: :wq
* Quit without saving: :q!

Open file at a specific line:

```bash
vim +26 ~/.bashrc
```

Add a new line below the current line:

* In command mode, press:

```text
o
```

Delete current line (command mode):

```text
dd
```

Paste below (command mode):

```text
p
```

---

## 4) Using wc (Word Count)

Default output counts:

1. lines
2. words
3. characters

```bash
wc <file>
```

Count words only:

```bash
wc -w <file>
```

Count lines only:

```bash
wc -l <file>
```

Count characters only:

```bash
wc -m <file>
```

Tip:

* Use lowercase letter l in wc -l
* wc -1 is invalid (that is number 1)

---

## Quick Troubleshooting

### "File exists" when creating a directory

This means a file or directory already uses that name.
Check:

```bash
ls -l <name>
```

If it is a file and you need a directory with the same name:

```bash
mv <name> <name>_old
mkdir <name>
```

### "Not a directory" when using cd

The target name is not a folder. Confirm with:

```bash
ls -l <name>
file <name>
```

### "No such file or directory"

You are in the wrong directory.
Check where you are:

```bash
pwd
ls
```

---

## Commands Summary

```bash
mkdir
touch
mv
cp
rm
rm -r
ls -la
chmod
chmod -R
nano
vim
wc
wc -w
wc -l
wc -m
pwd
cat
```


# Lab07: Linux CLI — Ep.2: Getting Started with the Terminal (Lab Brief)

## Purpose
Practice the basics of using the Linux terminal:
- entering commands correctly
- understanding successful vs unsuccessful output
- using parameters (flags)
- getting help using `--help` and `man`

## Key Ideas

### 1) Entering commands
Type a command at the prompt and press Enter to run it.
You can type when you see the cursor at the prompt.

Example prompt format:
username@computerName:path$
Example:
linux@commandline-intro:~$

`~` means home directory.
`$` means normal user, `#` means root.

### 2) Successful commands
Most successful commands return output.

Command:
ls

Example output:
commandline-intro  moretestfiles.txt  testdir  testfiles.csv

Meaning:
Lists files/folders in the current directory.

### 3) Unsuccessful commands
If you type a command wrong, you get an error.

Command (wrong):
Is

Example output:
bash: Is: command not found

Meaning:
Linux is case-sensitive. `Is` is not the same as `ls`.

### 4) Parameters (flags)
Flags change how a command works.
They usually start with `-` or `--`.

Examples:
ls -l
ls -a
ls -la
ls --help

You can chain short flags together:
ls -l -a  ==  ls -la

### 5) Example: detailed list including hidden files
Command:
ls -la

Example output includes:
- permissions
- owner/group
- file size
- timestamp
- file name

Hidden files start with a dot:
.bashrc
.profile
.config

### 6) Getting help
Use help text:
command --help
Example:
ls --help

Use manual pages (if installed):
man command
Example:
man ls

In `man`:
- use arrow keys to scroll
- press `q` to quit

## Commands to know (Ep.2)
- ls
- ls -la
- ls --help
- man ls

## What to do first in this lab 
- pwd
- ls
- ls -la
- ls --help
- man ls

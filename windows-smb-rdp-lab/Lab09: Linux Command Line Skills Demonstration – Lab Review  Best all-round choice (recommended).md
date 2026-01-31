# Lab09: **Linux CLI – Summary of Labs Covered**

## **Linux CLI: Ep.4 – Changing Things**

* Created and deleted files and directories
* Commands used:

  * `touch`, `mkdir`
  * `rm`, `rm -r`
  * `mv`, `cp`

---

## **Linux CLI: Ep.5 – File Permissions**

* Viewed and modified file permissions
* Learned permission formats (`rwx`)
* Commands used:

  * `ls -l`
  * `chmod` (e.g. `chmod 777 file`)
* Understood numeric permissions (700, 755, 777)

---

## **Linux CLI: Ep.6 – Editing Files**

* Edited files using terminal text editors
* Editors used:

  * `nano`
  * `vim`
* Key actions:

  * Save, exit, insert mode (Vim)

---

## **Linux CLI: Ep.7 – Using wc**

* Counted lines, words, and characters in files
* Commands used:

  * `wc`
  * `wc -l`, `wc -w`, `wc -m`

---

## **Linux CLI: Ep.8 – Manipulating Text**

* Modified file contents without editors
* Commands used:

  * `tr` (replace/remove characters)
  * `sed` (search and replace text)

---

## **Linux CLI: Ep.9 – Stream Redirection**

* Redirected command input/output
* Learned stdin, stdout, stderr
* Operators used:

  * `>`, `>>`
  * `1>`, `2>`
  * `2>/dev/null`

---

## **Linux CLI: Ep.10 – Using Sudo**

* Switched users and elevated privileges
* Commands used:

  * `sudo`
  * `sudo -i`
  * `su`, `su - user`
* Read protected system files

---

## **Linux CLI: Ep.11 – Using SSH and SCP**

* Connected to remote systems securely
* Transferred files between systems
* Commands used:

  * `ssh user@IP`
  * `scp`
  * SSH key authentication (`-i`)

---

## **Linux CLI: Ep.12 – Using Find**

* Searched for files across the system
* Filtered by:

  * Name
  * Owner
  * Permissions
* Commands used:

  * `find / -name file`
  * `find / -user user`
  * `find / -perm 777`

---

## **Linux CLI: Ep.13 – Searching and Sorting**

* Searched inside files and sorted results
* Commands used:

  * `grep`
  * `sort`, `sort -r`
* Combined commands with pipes

---

## **Linux CLI: Ep.14 – Using Screen**

* Managed persistent terminal sessions
* Commands used:

  * `screen -ls`
  * `screen -S name`
  * `screen -r name`
* Shortcuts:

  * Detach: `Ctrl + A` → `Ctrl + D`
  * Kill: `Ctrl + A` → `K` → `Y`

---

## **Linux CLI: Ep.15 – Generating File Hashes**

* Generated file hashes for integrity checking
* Hash types:

  * MD5
  * SHA1
  * SHA256
* Commands used:

  * `md5sum`
  * `sha1sum`
  * `sha256sum`
* Extracted first 4 hash characters

---

## **Linux CLI: Ep.16 – Combining Commands**

* Chained commands in one line
* Operators used:

  * `|` (pipe)
  * `&&`
  * `||`
  * `;`
  * `&` (background)

---

## **Linux CLI: Demonstrate Your Skills (Final Lab)**

* Applied all previous skills in one lab
* Tasks included:

  * File management
  * Permission changes
  * Hashing
  * Searching
  * SSH login
  * Sudo access
* Tokens generated after each task

---

### Final Takeaway

You now have **full foundational Linux CLI skills**, covering:

* File operations
* Permissions
* Searching & sorting
* Remote access (SSH)
* Privilege escalation
* Command chaining
* System administration basics


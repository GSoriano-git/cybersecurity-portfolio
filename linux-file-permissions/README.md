# File permissions in Linux

## Project description

This project demonstrates appropriate Linux commands to audit and manage file permissions within a Linux directory structure.

## Check file and directory details

The command to inspect permissions is: `ls -l`  

### Current file permissions
This document displays the file structure of the `/home/researcher2/projects` directory and the permissions of the files and subdirectory it contains.

In the `/home/researcher2/projects` directory, there are five files with the following names and permissions: 
* **project_k.txt**
  * User = read, write 
  * Group = read, write
  * Other = read, write
* **project_m.txt**
  * User = read, write
  * Group = read
  * Other = none
* **project_r.txt**
  * User = read, write
  * Group = read, write
  * Other = read
* **project_t.txt**
  * User = read, write
  * Group = read, write
  * Other = read
* **.project_x.txt**
  * User = read, write
  * Group = write
  * Other = none

There is also one subdirectory inside the `projects` directory named `drafts`. The permissions on `drafts` are:
* **drafts**
  * User = read, write, execute
  * Group = execute
  * Other = none

## Describe the permissions string

**Description:**  
Analyzing the output of `ls -l` reveals the initial access control configurations for the `/home/researcher2/projects` directory. The `drafts` directory is configured as `drwx--x---` (710), restricting traversal to the owner and group while blocking external access. The text files exhibit distinct access levels: `project_k.txt` is world-writable (`-rw-rw-rw-` / 666), `project_m.txt` is restricted to owner read/write and group read (`-rw-r-----` / 640), and both `project_r.txt` and `project_t.txt` grant read/write access to owner and group with read-only access for others (`-rw-rw-r--` / 664).

## Change file permissions

**Description:**  
Executes `chmod o-w project_k.txt` to revoke world-write access from an overly permissive file, reducing its permission string from `-rw-rw-rw-` (666) to `-rw-rw-r--` (664). This remediation secures the file against unauthorized modification by unprivileged users while preserving owner and group access. The modification is verified by executing `ls -l project_k.txt`.

## Change file permissions on a hidden file

**Description:**  
Executes `chmod u-w,g-w .project_x.txt` to strip write privileges from both the file owner and group, transitioning the hidden file from `-rw--w----` (620) to a read-only state (`-r--------` / 400). The `ls -la` command—utilizing the `-a` flag to list hidden entries—is run immediately after to verify the permission bit adjustment.

## Change directory permissions

**Description:**  
Executes `chmod g-x,o-rwx drafts` (or `chmod 700 drafts`) to strip group execute permissions and all external access from the subdirectory, hardening its state to `drwx------` (700). This modification prevents unauthorized users from traversing or viewing the directory contents. Verification is confirmed via `ls -la`.

## Summary

**Description:**  
This project covers auditing and remediating Linux file access controls using `ls` and `chmod`. Initial permission states were audited using `ls -l` for standard files and `ls -la` for hidden files and directory entries. Permission remediation was performed using target-specific `chmod` arguments: stripping world-write bits (`o-w`), hardening hidden files to read-only (`u-w,g-w`), and restricting directory traversal. Every modification was systematically verified using relative `ls` checks to confirm alignment with principle-of-least-privilege security policies.

**Full Documentation**
[View the Full Report Here:](File_permissions_in_Linux.pdf)

# File permissions in Linux

## Project description

This project is composed of different demonstration on appropriate Linux commands to manage file permissions on a Linux directory

## Check file and directory details

The command to show and check for permissions is: `ls -l`  
![][image1]

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

**Permission Analysis:** Executing `ls -l` reveals the access control configurations for the directory contents. The `drafts` directory is restricted with owner read/write/execute and group execute permissions (`drwx--x---`), while the text files exhibit varying levels of access: `project_k.txt` is world-writable (`-rw-rw-rw-`), `project_m.txt` is restricted strictly to the owner and group (`-rw-r-----`), and both `project_r.txt` and `project_t.txt` grant write access to the group with read-only access for others (`-rw-rw-r--`).    
![][image2]

## Change file permissions

**Permission Remediation:** Executing `chmod o-w project_k.txt` revokes write permissions for 'others' (world), hardening the file from an overly permissive state (`-rw-rw-rw-`) down to read-only for unprivileged users (`-rw-rw-r--`). The subsequent `ls -l` command verifies that world-write access was successfully stripped while maintaining standard owner and group access.    
![][image3]

## Change file permissions on a hidden file

**Hidden File Access Control:** Executing `chmod u-w,g-w .project_x.txt` revokes write access for both the file owner and the group, converting the hidden file into a strict read-only state (`-r--------`). The subsequent `ls -la` command—using the `-a` flag to reveal hidden files—verifies that write permissions were successfully stripped for both entities, leaving only owner read access.    
![][image4]

## Change directory permissions

**Directory Access Restriction & Hardening:** Executing the permission update strips all group and world permissions from the `drafts` directory, hardening its access state to `drwx------`. The resulting `ls -la` directory listing confirms that all access controls—read, write, and directory traversal (`x`)—have been completely revoked for both `research_team` group members and unprivileged external users, leaving the directory strictly isolated to the owner (`researcher2`).    
![][image5]  
![][image6]

## Summary

**Project Overview:** This project provides a practical demonstration of managing and auditing file access controls across a Linux directory structure using terminal commands.  
**Auditing Access Controls (`ls -l` & `ls -la`):** Used `ls -l` to analyze initial permission strings across standard files and `ls -la` to inspect hidden files (such as `.project_x.txt`) and directory traversal permissions (`.`).  
**Permission Remediation & Hardening (`chmod`):**

* **Unprivileged Access Removal:** Applied `chmod o-w project_k.txt` to strip world-write access, securing the file down to a read-only state for external users (`-rw-rw-r--`).  
* **Hidden File Isolation:** Executed `chmod u-w,g-w .project_x.txt` to revoke owner and group write permissions, locking the sensitive file into a strict read-only state (`-r--------`).  
* **Directory Access Restriction:** Utilized `chmod` to remove group and world permissions on the `drafts` directory (`drwx------`), preventing unauthorized users from entering or inspecting its contents.
**Verification Workflow:** Followed every `chmod` permission modification with a relative `ls -l` or `ls -la` audit to visually confirm that the targeted permission bits were successfully updated and aligned with security policies.

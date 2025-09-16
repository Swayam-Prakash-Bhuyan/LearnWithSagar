
## ✅ **Documentation Notes – `heist_notes.md`**

```
## Day 10 – The Filesystem Heist Notes

### Task 1 – Navigation
Used 'cd' with absolute and relative paths to explore directories, returning to home quickly using '~' shortcut.

### Task 2 – Hideout Setup
Created 'heist_vault', hidden files, and secured the directory with proper permissions.

### Task 3 – Storage Management
Simulated a new storage device using a loopback file, partitioned it, formatted it as ext4, mounted it at /data, and verified it using 'df -h' and 'lsblk'.

### Task 4 – File Operations
Copied, removed, and restored files including hidden files. Used brace expansion to create multiple directories. Managed permissions and cleaned up unwanted directories.

### Task 5 – Collaboration
Created a group and users, set up a shared space with group permissions and SGID, verified shared access by both users.

### Task 6 – Links
Explored hard and symbolic links, tested behavior when the original file is removed, and restored files using existing links.

### Task 7 – Archiving
Used 'tar', 'gzip', and 'bzip2' to archive and extract system directories safely, ensuring verification after each operation.

### Task 8 – Root Shell Operations
Escalated privileges, handled complex linking and compression scenarios, and learned how links behave after deletion.

## Challenges and Fixes:
- fdisk needed 'w' to save partitions; had to re-run after missing it.
- Hard link to /etc/passwd failed; used symbolic link instead.
- 'ls -R' output was too long; used 'less' to paginate.
- SGID bit behavior confirmed with group ownership inheritance.

## Takeaway:
These tasks helped reinforce filesystem navigation, security settings, file linking, and storage management—all essential skills for real-world SRE scenarios.
```

---

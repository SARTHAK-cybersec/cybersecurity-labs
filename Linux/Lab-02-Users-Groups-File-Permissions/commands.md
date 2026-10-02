# Linux Lab 02 — Commands Documentation

This document records the Linux commands used during the Users, Groups & File Permissions investigation.

---

## 1. Identify Current User

```bash
whoami
```

**Purpose:** Displays the username of the current effective user.

---

## 2. Investigate User and Group Information

```bash
id
```

**Purpose:** Displays the user's UID, primary GID, and supplementary group memberships.

```bash
groups
```

**Purpose:** Displays the groups associated with the current user.

---

## 3. Investigate Specific Groups

```bash
getent group eminem
```

**Purpose:** Retrieves information about the `eminem` group from the system's configured group databases.

```bash
getent group sudo
```

**Purpose:** Checks membership of the `sudo` group.

---

## 4. Investigate `/etc/passwd`

```bash
grep "^eminem:" /etc/passwd
```

**Purpose:** Searches for the `eminem` account entry in `/etc/passwd`.

---

## 5. Investigate `/etc/shadow`

```bash
sudo grep "^eminem:" /etc/shadow
```

**Purpose:** Accesses the protected account entry in `/etc/shadow`.

**Security note:** Password hashes from `/etc/shadow` should never be published in a public repository.

---

## 6. Examine File Permissions

```bash
ls -l ~/cyber-labs/linux-lab-01/suspicious/temp_data.txt
```

**Purpose:** Displays the file's permissions, ownership, size, and modification time.

---

## 7. Examine Detailed File Metadata

```bash
stat ~/cyber-labs/linux-lab-01/suspicious/temp_data.txt
```

**Purpose:** Displays detailed metadata including:

- File size
- Inode
- Number of links
- UID
- GID
- Access time
- Modification time
- Change time
- Birth time

---

## 8. Create the Permission Test Environment

```bash
mkdir -p ~/cyber-labs/linux-lab-02/permissions
```

**Purpose:** Creates the directory used for permission experiments.

```bash
cd ~/cyber-labs/linux-lab-02/permissions
```

**Purpose:** Moves into the permission-testing directory.

```bash
touch testfile.txt
```

**Purpose:** Creates an empty test file.

---

## 9. Inspect Test File Permissions

```bash
ls -l testfile.txt
```

**Purpose:** Displays the current permissions and ownership of the test file.

---

## 10. Remove Write Permissions

```bash
chmod a-w testfile.txt
```

**Purpose:** Removes write permission from the owner, group, and others.

---

## 11. Restore Owner Write Permission

```bash
chmod u+w testfile.txt
```

**Purpose:** Adds write permission for the file owner.

---

## 12. Test File Modification

```bash
echo "authorized test" >> testfile.txt
```

**Purpose:** Appends text to the file to test whether the current user has write permission.

```bash
cat testfile.txt
```

**Purpose:** Displays the file contents.

---

## 13. Numeric Permission Testing

### Set permissions to 600

```bash
chmod 600 testfile.txt
```

### Set permissions to 644

```bash
chmod 644 testfile.txt
```

### Set permissions to 755

```bash
chmod 755 testfile.txt
```

**Purpose:** Demonstrates how numeric permission values modify access for the owner, group, and others.

---

## 14. Change File Ownership

```bash
sudo chown root:root testfile.txt
```

**Purpose:** Changes the file owner and group to `root`.

---

## 15. Test Unauthorized Modification

```bash
echo "normal user attempt" >> testfile.txt
```

**Purpose:** Tests whether the normal user can modify a file owned by `root`.

Expected result in this lab:

```text
permission denied
```

---

## 16. Perform Privileged Modification

```bash
sudo sh -c 'echo "sudo modification" >> testfile.txt'
```

**Purpose:** Executes the modification command with elevated privileges.

---

## 17. Verify File Contents

```bash
cat testfile.txt
```

**Purpose:** Confirms whether the modification succeeded.

---

## 18. Enumerate Sudo Privileges

```bash
sudo -l
```

**Purpose:** Displays the commands the current user is permitted to execute through `sudo`.

---

## Permission Reference

Linux permissions use three basic permission bits:

```text
r = read
w = write
x = execute
```

Numeric values:

```text
r = 4
w = 2
x = 1
```

Examples:

```text
600 = rw-------
644 = rw-r--r--
664 = rw-rw-r--
755 = rwxr-xr-x
```

The three numeric positions represent:

```text
Owner | Group | Others
```

---

## Important Security Notes

- Do not publish real password hashes.
- Do not perform permission experiments on important system files.
- Use a controlled lab environment when testing ownership and permissions.
- `sudo` provides elevated privileges and should be used carefully.
- File ownership and permissions should always be considered when investigating unauthorized access or suspicious files.

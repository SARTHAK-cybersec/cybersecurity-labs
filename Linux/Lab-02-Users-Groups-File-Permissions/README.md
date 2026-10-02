# Linux Cybersecurity Lab 02 — Users, Groups & File Permissions

## Overview

This lab focuses on Linux identity, user and group management, file ownership, file permissions, `chmod`, `chown`, and `sudo`.

The purpose of this lab was to understand how Linux controls access to files and how permissions and privileges are important during cybersecurity investigations.

---

## Objectives

- Identify the current Linux user and user ID
- Investigate user and group memberships
- Understand `/etc/passwd` and `/etc/shadow`
- Examine file ownership and permissions
- Understand numeric Linux permissions
- Practice `chmod`
- Practice `chown`
- Investigate permission-denied events
- Understand privileged operations with `sudo`
- Examine sudo privileges using `sudo -l`
- Use `stat` to investigate file metadata

---

## Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux Rolling 2026.2 |
| Username | `eminem` |
| Virtualization | VirtualBox |
| Shell | Zsh |
| Lab Type | Local Linux Security Lab |

---

## Lab Structure

```text
Lab-02-Users-Groups-File-Permissions/
├── README.md
├── commands.md
├── findings.md
└── screenshots/
    ├── 01-user-group-investigation.png
    ├── 02-passwd-shadow-investigation.png
    ├── 03-file-ownership-permissions.png
    ├── 04-chmod-permission-investigation.png
    └── 05-ownership-and-sudo-investigation.png
```

---

## 1. User and Group Investigation

The current user and group memberships were investigated using:

```bash
whoami
id
groups
```

The account used for this lab was:

```text
eminem
```

The account had membership in several groups, including:

- `sudo`
- `adm`
- `wireshark`
- `netdev`
- `vboxsf`

Group membership can affect what resources and administrative capabilities a user has access to.

---

## 2. `/etc/passwd` and `/etc/shadow`

The account information was investigated using:

```bash
grep "^eminem:" /etc/passwd
```

The protected shadow database was accessed with:

```bash
sudo grep "^eminem:" /etc/shadow
```

The `/etc/passwd` file contains account and user information, while `/etc/shadow` contains protected password-related information.

The password hash was **not included in this repository**.

---

## 3. File Ownership and Permissions

An existing suspicious file from Linux Lab 01 was investigated:

```text
~/cyber-labs/linux-lab-01/suspicious/temp_data.txt
```

Initial permissions and ownership:

```text
-rw-rw-r-- 1 eminem eminem 21 ...
```

The numeric permission value was:

```text
664
```

This means:

```text
Owner  → read + write
Group  → read + write
Others → read
```

File metadata was also examined using:

```bash
stat ~/cyber-labs/linux-lab-01/suspicious/temp_data.txt
```

---

## 4. Permission Testing with `chmod`

A test file was used to safely experiment with Linux permissions.

Different permission modes were tested:

### 600

```text
-rw-------
```

Only the owner has read and write permissions.

### 644

```text
-rw-r--r--
```

The owner can read and write, while group and others can only read.

### 755

```text
-rwxr-xr-x
```

The owner has read, write, and execute permissions, while group and others have read and execute permissions.

These tests demonstrated how changing permission bits directly affects file access.

---

## 5. Ownership Testing with `chown`

The ownership of the test file was changed using:

```bash
sudo chown root:root testfile.txt
```

After the change, the file was owned by:

```text
root:root
```

Although the file remained accessible for reading, the normal user could no longer modify it because the user was no longer the file owner and the applicable permissions did not allow writing.

---

## 6. Permission-Denied Investigation

A normal modification attempt was performed:

```bash
echo "normal user attempt" >> testfile.txt
```

The operation failed with:

```text
permission denied
```

This demonstrated that Linux checks the effective user's permissions against the file's owner, group, and other permissions before allowing an operation.

---

## 7. Privileged Modification with `sudo`

A privileged modification was then performed:

```bash
sudo sh -c 'echo "sudo modification" >> testfile.txt'
```

The modification succeeded because the command was executed with elevated privileges.

The resulting contents were verified using:

```bash
cat testfile.txt
```

This demonstrated the difference between normal user permissions and privileged administrative access.

---

## 8. Sudo Privilege Investigation

The user's available sudo privileges were examined using:

```bash
sudo -l
```

The lab environment reported:

```text
(ALL : ALL) ALL
```

This indicates that the account is configured with broad sudo privileges.

From a cybersecurity perspective, unrestricted administrative privileges are important to investigate because an account with elevated privileges can perform sensitive system-level operations.

---

## Security Concepts Demonstrated

This lab provided hands-on practice with:

- Linux users
- UIDs and GIDs
- Groups
- File ownership
- File permissions
- Permission bits
- Numeric `chmod`
- Symbolic permissions concepts
- `chown`
- Protected account information
- Permission-denied events
- Privilege escalation concepts
- `sudo`
- Sudo privilege enumeration
- File metadata investigation

---

## Key Takeaway

Linux access control is based on multiple layers, including:

```text
User Identity
      ↓
Group Membership
      ↓
File Ownership
      ↓
File Permissions
      ↓
Privileged Access
```

Understanding these controls is essential for investigating suspicious files, unauthorized access, privilege abuse, and system security incidents.

---

## Disclaimer

This lab was performed in a controlled personal Kali Linux virtual machine for cybersecurity learning and practice.

# Linux Lab 02 — Findings & Security Analysis

## Investigation Summary

This lab investigated Linux users, groups, file ownership, permissions, and privileged access in a controlled Kali Linux environment.

The investigation demonstrated how Linux access control determines whether a user can read, modify, or execute a file.

---

## Finding 01 — Current User and Group Membership

The investigation identified the current user as:

```text
eminem
```

The account had membership in several groups, including:

```text
sudo
adm
wireshark
netdev
```

### Security Significance

Group membership can provide additional access to system resources.

Of particular interest was membership in the `sudo` group because it allows the account to use configured sudo privileges.

In a security investigation, unexpected group membership can be an important indicator to investigate further.

---

## Finding 02 — Protected Password Information

The `/etc/passwd` account entry could be read without elevated privileges.

Accessing the corresponding `/etc/shadow` entry without sufficient privileges resulted in:

```text
Permission denied
```

Access through `sudo` succeeded.

### Security Significance

Linux protects `/etc/shadow` because it contains sensitive password-related information.

This demonstrates an important principle of Linux security:

> Sensitive system information should have restricted access.

The password hash obtained during testing was not stored in this repository.

---

## Finding 03 — File Ownership and Permissions

The suspicious file from Lab 01 was:

```text
~/cyber-labs/linux-lab-01/suspicious/temp_data.txt
```

Its permissions were:

```text
-rw-rw-r--
```

Numeric representation:

```text
664
```

Ownership:

```text
eminem:eminem
```

### Interpretation

The owner could:

```text
read
write
```

The group could:

```text
read
write
```

Others could:

```text
read
```

### Security Significance

File ownership and permissions determine who can interact with a file.

When investigating suspicious files, ownership should therefore be checked alongside the file's contents and timestamps.

---

## Finding 04 — Permission Changes Affect Access

The test file was assigned several permission configurations:

```text
600 → rw-------
644 → rw-r--r--
755 → rwxr-xr-x
```

### Observation

Changing the permission bits changed the access available to the owner, group, and other users.

This demonstrated that Linux does not treat file access as simply "allowed" or "blocked." Access depends on the combination of:

```text
User identity
+
Group membership
+
File ownership
+
Permission bits
```

---

## Finding 05 — Ownership Affects Permission Management

The test file was changed from:

```text
eminem:eminem
```

to:

```text
root:root
```

After this change, an attempt by the normal user to modify the file failed.

The user also attempted to change the permissions using `chmod`, but the operation failed because the user no longer owned the file.

### Security Significance

This demonstrated an important Linux security relationship:

```text
File Ownership
       ↓
Determines which user can normally manage permissions
```

Ownership should therefore be examined when investigating unexpected permission changes.

---

## Finding 06 — Normal User vs Privileged Access

After the file was owned by `root`, a normal modification attempt failed:

```text
permission denied
```

A privileged modification using:

```bash
sudo sh -c 'echo "sudo modification" >> testfile.txt'
```

succeeded.

### Security Significance

The result demonstrates the difference between normal user access and privileged administrative access.

A user with broad sudo privileges can perform operations that would otherwise be denied.

During incident response, investigators should therefore examine:

- Which account performed an action
- Whether the account had sudo privileges
- Which files were modified
- File ownership
- File timestamps
- Relevant authentication and system logs

---

## Finding 07 — Broad Sudo Privileges

The command:

```bash
sudo -l
```

reported:

```text
(ALL : ALL) ALL
```

### Interpretation

The account is configured to use sudo for commands as permitted by the system's sudo configuration.

### Security Significance

Broad administrative privileges increase the potential impact if an account is compromised.

For defensive security investigations, sudo configuration and privileged activity should therefore be reviewed when investigating suspicious behavior.

---

## Evidence Collected

The following screenshots were captured during the investigation:

| Evidence | Description |
|---|---|
| `01-user-group-investigation.png` | User identity and group membership |
| `02-passwd-shadow-investigation.png` | `/etc/passwd` and protected `/etc/shadow` investigation |
| `03-file-ownership-permissions.png` | File ownership, permissions, and metadata |
| `04-chmod-permission-investigation.png` | Permission changes using `chmod` |
| `05-ownership-and-sudo-investigation.png` | Ownership change, denied access, sudo modification, and sudo privileges |

---

## Overall Security Observations

This lab demonstrated several fundamental Linux security concepts:

1. **Identity matters** — Linux evaluates access based on the effective user.
2. **Groups matter** — Group membership can provide additional access.
3. **Ownership matters** — File owners have special control over their files.
4. **Permissions matter** — `r`, `w`, and `x` determine allowed operations.
5. **Sudo matters** — Privileged access can bypass restrictions that apply to normal users.
6. **Metadata matters** — Timestamps, ownership, permissions, and inode information can support forensic investigation.
7. **Sensitive files require protection** — `/etc/shadow` demonstrates how Linux restricts access to sensitive information.

---

## Investigation Limitation

The presence of a suspicious file or unusual permission does not by itself prove that a system has been compromised.

A real investigation would require additional evidence such as:

- Authentication logs
- Process information
- Network connections
- Shell history
- System logs
- File hashes
- Persistence mechanisms
- Timeline analysis

Therefore, the findings in this lab demonstrate security concepts and investigative techniques rather than confirming an actual security incident.

---

## Conclusion

The investigation provided hands-on experience with Linux access control and privilege management.

The most important practical lesson was that **user identity, group membership, ownership, permissions, and privileged access must be considered together when analyzing file access and suspicious activity**.

This knowledge provides a foundation for future cybersecurity work involving Linux hardening, SOC investigations, incident response, and digital forensics.

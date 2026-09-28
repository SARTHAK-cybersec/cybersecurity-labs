# Lab 01 — File & Directory Investigation

## Overview

This lab is a beginner-level Linux cybersecurity investigation performed in a controlled Kali Linux virtual machine environment.

The purpose of the lab was to practice basic Linux file-system investigation, log analysis, suspicious-file identification, and evidence collection.

The lab uses simulated security-related data rather than real production-system data.

---

## Objectives

The main objectives of this lab were:

- Understand Linux files and directories
- Create an organized investigation workspace
- Investigate authentication logs
- Identify failed and successful login attempts
- Search for suspicious files
- Examine file contents
- Identify file types
- Check file sizes
- Practice basic evidence-based investigation

---

## Environment

| Item | Details |
|---|---|
| Operating System | Kali GNU/Linux Rolling |
| Version | 2026.2 |
| Environment | VirtualBox |
| Lab Type | Local simulated cybersecurity lab |
| User | `eminem` |

---

## Lab Directory Structure

```text
linux-lab-01/
├── logs/
│   ├── auth.log
│   └── system.log
├── evidence/
│   └── notes.txt
└── suspicious/
    └── temp_data.txt

# Investigation Scenario:-

A small Linux investigation environment was created containing authentication logs, evidence files, and a suspicious directory.

The objective was to examine the available files and identify potentially interesting security-related information.

The investigation focused on:

Authentication activity
Suspicious files
File metadata
File contents
Basic evidence collection
Investigation Process



1. Created the investigation workspace

The following directories were created:
logs/
evidence/
suspicious/
These directories were used to separate different types of investigation data.


2. Investigated authentication logs

The file:

logs/auth.log

was examined to identify authentication activity.

The log contained:

Successful login: eminem
Failed login: unknown_user
Failed login: unknown_user
Successful login: eminem


The investigation identified:


Successful login attempts: 2
Failed login attempts: 2


3. Investigated the suspicious directory

The suspicious directory was searched for files.

##The following file was identified:

suspicious/temp_data.txt

The file was initially empty and was later populated with simulated suspicious data for investigation.


4. Examined the suspicious file


The file contained:

unknown process data

The file was identified as:

ASCII text

The file size was approximately:

21 bytes

##Key Findings

Finding	Result

Successful login attempts	2

Failed login attempts	2

Suspicious non-empty files	1

Suspicious file	suspicious/temp_data.txt

File type	ASCII text

File content	unknown process data


##Conclusion

The investigation identified two failed authentication attempts and one non-empty file located in the suspicious directory.

The available evidence does not by itself prove that a system compromise occurred. Additional investigation would be required to determine the source and significance of the activity.

This lab provided practical experience with Linux file-system navigation, log analysis, text searching, file identification, and basic cybersecurity investigation methodology.

<>Skills Practiced

Linux command-line navigation

File and directory management

Linux file-system investigation

Basic log analysis

Text searching with grep

File discovery with find

File-type identification

Basic evidence collection

Security investigation methodology

##Commands Used

The commands used during the investigation are documented separately in commands.md.

Detailed investigation findings are documented in findings.md.

##Disclaimer

This is a self-created educational cybersecurity lab performed in a controlled local environment. The authentication events and suspicious file were simulated for learning purposes.

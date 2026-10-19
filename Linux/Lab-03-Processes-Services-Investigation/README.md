# Lab 03 — Linux Processes & Services Investigation

## Overview

This lab investigates Linux processes, systemd services, system logs, listening sockets, Unix-domain sockets, and system resource usage in a Kali Linux virtual machine.

The goal is to practise basic host-investigation techniques used in cybersecurity operations and learn how to interpret system evidence without assuming that an unfamiliar process is malicious.

## Objectives

- Enumerate running processes and understand PID, PPID, process owner, and process state.
- Inspect a service's status, logs, unit definition, and effective configuration.
- Check TCP/UDP listening sockets and local Unix-domain sockets.
- Investigate an SSH agent and verify its executable path, identity information, open file descriptors, and socket permissions.
- Review CPU usage, memory consumption, swap usage, and system load.
- Document findings and distinguish observations from security conclusions.

## Environment

- Operating system: Kali Linux
- Virtualization: Oracle VirtualBox
- Shell: Zsh
- User account: `eminem`

## Tools and Commands

- `ps` — process enumeration and resource usage
- `pgrep` — process lookup
- `systemctl` — service status and configuration inspection
- `journalctl` — service-log review
- `ss` — socket inspection
- `/proc` — kernel-provided process information
- `ssh-add` — SSH agent identity inspection
- `free` — memory and swap usage
- `uptime` — system uptime and load averages
- `nproc` — available processing units

## Investigation Summary

### 1. Process Investigation

Enumerated running processes and examined process IDs, parent process IDs, owners, states, and command lines.

### 2. NetworkManager Service

Reviewed the service's status, recent logs, unit definition, and effective configuration. The captured logs showed network activation and DHCP configuration activity. No warning-level entries were returned by the selected journal query.

### 3. Listening Sockets

Checked TCP and UDP listening sockets using `ss`. No TCP/UDP listening sockets were listed at the time of the check.

Inspected Unix-domain sockets and observed endpoints associated with system and desktop components, including an SSH agent.

### 4. SSH Agent Investigation

Investigated the running `ssh-agent` process, including its executable path, process status, user and parent IDs, loaded identities, open file descriptors, and Unix socket.

The executable resolved to `/usr/bin/ssh-agent`. The agent reported no loaded identities. Its socket was owned by `eminem` and had restrictive owner-only permissions.

The observations were consistent with a user-level SSH agent. No clear indicator of malicious activity was identified in the checks performed.

### 5. Resource Usage

Reviewed the processes with the highest CPU and memory usage. The leading entries in the captured snapshots were recognizable Kali desktop components.

The system reported approximately 3.8 GiB of RAM, 3.0 GiB available memory, no swap in use, two available processing units, and low load averages.

## Security Assessment

The evidence collected during this lab did not reveal a clear indicator of malicious activity in the specific processes, service logs, sockets, and resource snapshots examined.

This is a limited assessment of a lab environment, not a comprehensive security audit. Process names, executable paths, permissions, and resource usage must be interpreted in context and may require additional verification.

## Evidence

Screenshots documenting the investigation will be stored in the `screenshots/` directory.

## Key Learning Outcomes

- Understanding process ancestry and ownership.
- Inspecting systemd services and their logs.
- Differentiating network listening sockets from local IPC sockets.
- Investigating SSH agent metadata and socket permissions.
- Interpreting resource metrics without treating them as standalone indicators of compromise.
- Recording evidence-based findings with appropriate limitations.

## Disclaimer

This lab was conducted in a personal Kali Linux virtual machine for educational purposes.

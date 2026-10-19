# Lab 03 — Investigation Findings

## 1. Objective

Investigate Linux processes, services, sockets, the SSH agent, and system resource usage in a Kali Linux virtual machine. Record observations and avoid classifying activity as malicious without sufficient evidence.

## 2. Process Investigation

**Observations**
- Used `ps` and `ps aux` to enumerate processes.
- Examined process IDs (PID), parent process IDs (PPID), process owners, states, and command lines.
- Observed system and desktop processes, including `systemd-journald`, `NetworkManager`, `cron`, Xorg, and XFCE components.

**Assessment**

The captured process listings did not establish a clear indicator of malicious activity. A process name or owner alone is insufficient to determine whether a process is legitimate.

## 3. NetworkManager Service

**Observations**
- The service was reported as `active (running)` by `systemctl`.
- Its executable command was `/usr/sbin/NetworkManager --no-daemon`.
- Logs showed network activation, DHCP configuration, and related network setup activity.
- The selected warning-level journal query returned no entries.

**Assessment**

The observed service status and log activity were consistent with normal network management in the lab environment. The empty warning-level query means no matching entries were returned for the selected time range; it does not prove that the system has no security issues.

## 4. Listening Sockets

**Observations**
- `sudo ss -lntup` returned no listed TCP/UDP listening sockets at the time of the captured check.
- `sudo ss -lxp` displayed Unix-domain sockets associated with local system and desktop components.

**Assessment**

No TCP/UDP listeners were listed in that particular snapshot. Unix-domain sockets provide local inter-process communication and should not be confused with network listening ports. Socket names and paths alone do not establish whether activity is safe or malicious.

## 5. SSH Agent Investigation

**Observations**
- The process was identified as `ssh-agent`.
- The executable path was verified as `/usr/bin/ssh-agent`.
- The process ran under the `eminem` account and had PPID 1.
- `ssh-add -l` reported that the agent had no identities loaded.
- File-descriptor inspection showed a socket associated with the process.
- The agent's Unix socket was owned by `eminem` and had owner-only permissions (`srw-------`).

**Assessment**

These observations were consistent with a user-level SSH agent. No clear indicator of malicious activity was identified in the checks performed. An empty agent identity list is not itself evidence of compromise, and the process should be reassessed if its behavior or context changes.

## 6. Resource Usage

**Observations**
- The highest CPU and memory entries in the captured snapshots included Xorg and XFCE desktop components.
- `free -h` reported approximately 3.8 GiB of RAM, with approximately 3.0 GiB available.
- No swap was in use at the time of measurement.
- `nproc` reported two available processing units.
- `uptime` showed low load averages in the captured snapshot.

**Assessment**

The collected snapshot did not show obvious resource exhaustion. Resource consumption changes over time, so a single measurement cannot rule out intermittent or hidden activity.

## 7. Overall Conclusion

The investigation did not identify a clear indicator of malicious activity within the specific processes, NetworkManager logs, sockets, SSH agent metadata, and resource snapshots examined.

This conclusion is limited to the evidence collected. It is not a guarantee that the machine is secure or a substitute for a comprehensive security audit.

## 8. Limitations

- Findings describe a particular lab session and may change after reboot.
- Process IDs, socket paths, and resource measurements are session-specific.
- The investigation focused on selected commands and components.
- No full malware scan, forensic disk analysis, or comprehensive incident-response investigation was performed.

## 9. Skills Practised

- Linux process enumeration and process metadata analysis.
- systemd service and journal inspection.
- TCP/UDP listener and Unix-domain socket inspection.
- SSH agent and socket-permission investigation.
- CPU, memory, swap, and load interpretation.
- Evidence-based documentation with explicit limitations.

## Disclaimer

This investigation was conducted in a personal Kali Linux virtual machine for educational purposes.

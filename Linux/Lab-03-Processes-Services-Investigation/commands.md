# Lab 03 — Commands Reference

This document records the Linux commands used during the Processes & Services Investigation.

## 1. Process Enumeration

### List running processes

```bash
ps
```

### Display processes with detailed information

```bash
ps aux
```

### Display a short process snapshot

```bash
ps aux | head -15
```

### Inspect PID, PPID, owner, state, and command

```bash
ps -eo pid,ppid,user,stat,comm --sort=pid | head -20
```

### Inspect the current shell

```bash
ps -p $$ -o pid,ppid,user,stat,comm
```

## 2. Service Investigation

### Check NetworkManager status

```bash
systemctl status NetworkManager --no-pager
```

### Review recent service logs

```bash
sudo journalctl -u NetworkManager --since "1 hour ago" --no-pager -n 20
```

### Review warning-level service logs

```bash
sudo journalctl -u NetworkManager -p warning --since "24 hours ago" --no-pager
```

### Inspect the service unit definition

```bash
systemctl cat NetworkManager
```

### Inspect selected effective service properties

```bash
systemctl show NetworkManager -p FragmentPath -p DropInPaths -p ExecStart -p User -p Restart
```

## 3. Socket Investigation

### List TCP and UDP listening sockets

```bash
sudo ss -lntup
```

### List Unix-domain sockets

```bash
sudo ss -lxp
```

### Search socket information for a process or socket inode

```bash
sudo ss -xapne | grep -E 'pid=1093|9644'
```

The PID and socket inode in this example came from the observed SSH agent and may change between sessions.

## 4. SSH Agent Investigation

### Find SSH agent processes

```bash
pgrep -a ssh-agent
```

### Inspect process metadata

```bash
ps -p 1093 -o pid,ppid,user,stat,lstart,etime,args
```

### Verify the executable path

```bash
sudo ls -l /proc/1093/exe
```

### Check loaded SSH identities

```bash
ssh-add -l
```

### Inspect process status

```bash
cat /proc/1093/status | head -20
```

### Inspect open file descriptors

```bash
sudo ls -l /proc/1093/fd
```

### Inspect the SSH agent socket permissions

```bash
ls -l /home/eminem/.ssh/agent/s.a68rRt86x2.agent.oNX8njIGZT
```

The PID, socket path, and inode are session-specific examples from this investigation. Re-identify them before reusing these commands on another session or machine.

## 5. Resource Investigation

### Show processes sorted by CPU usage

```bash
ps aux --sort=-%cpu | head -10
```

### Show processes sorted by memory usage

```bash
ps aux --sort=-%mem | head -10
```

### Display memory and swap usage

```bash
free -h
```

### Display uptime and load averages

```bash
uptime
```

### Count available processing units

```bash
nproc
```

## Notes

- Commands that inspect protected process information or system sockets may require `sudo`.
- Use `--no-pager` when you want command output to return directly to the terminal.
- PIDs, socket inodes, paths, and resource values may change after a reboot or between sessions.
- A command's output must be interpreted in context. An unfamiliar process or socket is not automatically malicious.

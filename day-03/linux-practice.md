# Linux Practice Guide

**Essential commands, their uses, and real-world troubleshooting**  
Use this as a quick reference when checking processes, services, logs, and network connectivity.

## A3 visual cheat sheets

### Landscape poster

![Linux Practice Guide — A3 landscape](linux-practice-guide-a3-landscape.png)

### Portrait poster

![Linux Practice Guide — A3 portrait](linux-practice-guide-a3-portrait.png)

---

## 1. Process checks

| Command | Use / purpose |
|---|---|
| `ps aux` | View all running processes. |
| `top` | Monitor processes and system usage in real time. |
| `htop` | Interactive process viewer. |
| `pgrep <name>` | Find a process ID (PID) by name. |
| `pkill <name>` | Send a signal to processes by name. |
| `kill <PID>` | Send the default termination signal to a process. |
| `kill -9 <PID>` | Force-kill a process when necessary. |
| `jobs` | List background jobs in the current shell. |
| `bg` | Resume a stopped job in the background. |
| `fg` | Bring a background job to the foreground. |

## 2. Service checks

Replace `<service>` with a service name, such as `nginx` or `ssh`.

| Command | Use / purpose |
|---|---|
| `systemctl status <service>` | Check service status. |
| `systemctl start <service>` | Start a service. |
| `systemctl stop <service>` | Stop a service. |
| `systemctl restart <service>` | Restart a service. |
| `systemctl enable <service>` | Enable a service to start at boot. |
| `systemctl disable <service>` | Disable a service from starting at boot. |
| `service <name> status` | Check service status on systems using the legacy `service` command. |
| `service <name> start` | Start a service on systems using the legacy `service` command. |
| `service <name> stop` | Stop a service on systems using the legacy `service` command. |
| `systemctl list-units --type=service` | List loaded service units. |

## 3. Log checks

| Command | Use / purpose |
|---|---|
| `journalctl` | View systemd journal logs. |
| `journalctl -f` | Follow journal logs in real time. |
| `journalctl -u <service>` | View logs for a specific service. |
| `tail -f /var/log/syslog` | Follow a syslog file in real time (on systems using this path). |
| `tail -n 50 /var/log/auth.log` | Show the last 50 lines of the authentication log (if present). |
| `grep "error" /var/log/syslog` | Search the syslog for the word `error`. |
| `dmesg` | View kernel messages. |
| `less /var/log/syslog` | Read a log file page by page (if present). |
| `cat /var/log/syslog` | Print a log file's contents. |
| `sudo journalctl --since "1 hour ago"` | View journal entries from the last hour. |

## 4. Networking checks

| Command | Use / purpose |
|---|---|
| `ip addr` | Show network interfaces and IP addresses. |
| `ip route` | View the routing table. |
| `ping <host>` | Test connectivity to a host. |
| `traceroute <host>` | Trace the route packets take to a host. |
| `dig <domain>` | Query DNS records. |
| `nslookup <domain>` | Perform a DNS query. |
| `curl -I <url>` | Check HTTP response headers from a URL. |
| `netstat -tulnp` | Show listening ports (if `net-tools` is installed). |
| `ss -tulnp` | Show listening sockets and associated processes (where permissions allow). |
| `ifconfig` | View network interface details on older systems (if `net-tools` is installed). |

## 5. Mini troubleshooting workflow

1. **Check the process:** Is the application running? Try `ps aux`, `top`, or `pgrep <name>`.
2. **Check the service:** Is the service active? Try `systemctl status <service>`.
3. **Check the logs:** Look for errors with `journalctl -u <service> -n 50`, `tail`, or `grep`.
4. **Check the network:** Verify addresses and routes with `ip addr` and `ip route`; test reachability with `ping <host>`.
5. **Take action:** Based on the evidence, correct the configuration, investigate firewall or dependency issues, or restart the service if appropriate.

## Quick reference tips

- Use `man <command>` to read a command's manual.
- Use `command --help` for a quick option summary when supported.
- Check logs before restarting a service.
- Prefer `ss` over `netstat` on modern Linux systems.
- Use `kill -9` only as a last resort; it does not allow a process to clean up.
- Some commands require installation or elevated privileges (`sudo`). Log file paths vary by Linux distribution.

> **Remember:** Observe → Diagnose → Fix → Verify. Practice commands in a lab before using them on production servers.

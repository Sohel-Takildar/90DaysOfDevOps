# Linux Commands Cheat Sheet

## Process Management Commands

| Command |                        | Usage |
|                                  |
| `ps aux`                         | Show all running processes |
| `top`                            | Real-time system process monitor |
| `htop`                           | Interactive process viewer |
| `kill PID`                       | Terminate a process by PID |
| `killall process_name`           | Kill all processes by name |
| `pkill process_name`             | Kill process using process name |
| `jobs`                           | Show background jobs |
| `bg`                             | Resume a job in background |
| `fg`                             | Bring background job to foreground |
| `nice -n 10 command`             | Start process with priority |
| `renice priority PID`            | Change running process priority |

---

## File System Commands

| Command |                        | Usage |
|                                  |
| `pwd`                            | Show current directory |
| `ls -la`                         | List files with details |
| `cd /path`                       | Change directory |
| `mkdir folder`                   | Create new directory |
| `rm -rf folder`                  | Remove directory and contents |
| `cp source dest`                 | Copy files/directories |
| `mv old new`                     | Move or rename files |
| `touch file.txt`                 | Create empty file |
| `cat file.txt`                   | View file contents |
| `nano file.txt`                  | Edit file using nano editor |
| `find / -name file.txt`          | Search for a file |
| `df -h`                          | Show disk space usage |
| `du -sh folder`                  | Show folder size |
| `chmod 755 file.sh`              | Change file permissions |
| `chown user:user file.txt`       | Change file ownership |

---

## Networking Troubleshooting Commands

| Command |                        | Usage |
|                                  |
| `ping google.com`                | Check network connectivity |
| `ip addr`                        | Show IP addresses |
| `curl https://example.com`       | Fetch website response |
| `dig google.com`                 | DNS lookup information |
| `netstat -tulnp`                 | Show listening ports |
| `ss -tulnp`                      | Display active connections |
| `traceroute google.com`          | Trace packet route |
| `wget URL`                       | Download files from internet |
| `hostname -I`                    | Show system IP address |
| `nslookup domain.com`            | Query DNS records |

---

## Log & System Monitoring Commands

| Command |                        | Usage |
|                                  |
| `journalctl -xe`                 | View system logs |
| `tail -f /var/log/syslog`        | Monitor logs live |
| `free -h`                        | Show memory usage |
| `uptime`                         | Display system uptime |
| `whoami`                         | Show current logged-in user |
| `uname -a`                       | Show system information |



# Quick Tips

- Use `man command_name` to read command manuals.
- Add `--help` with most commands for quick help.
- Combine commands using pipes `|` for powerful troubleshooting.

Example:
```bash
ps aux | grep nginx

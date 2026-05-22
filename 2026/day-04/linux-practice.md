# Day 04 – Linux Practice: Processes and Services

## 1. Process Checks

### 1. Check Running Processes
```bash
      ' ps aux | head '

## 2. Monitor Live Processes
      ' top '

## 3. Find Process by Name
      ' pgrep sshd '

## 4. Check Docker Service Status
     ' systemctl status docker '

## 5. List Running Services
     ' systemctl list-units --type=service --state=running '

## 6. View Docker Logs
     ' journalctl -u docker --no-pager | tail -n 10 '

## 7. Check System Logs
     ' tail -n 20 /var/log/syslog '


##### Mini Troubleshooting Steps
Scenario

Docker containers were not starting properly.

Troubleshooting Performed

## Step 1: Check Docker Service
systemctl status docker

Result:

Docker service was active and running

## Step 2: Check Docker Logs
journalctl -u docker --no-pager | tail -n 20

Result:

No critical errors found in logs

## Step 3: Verify Docker Process
ps aux | grep docker

Result:

Docker daemon process was running correctly

# ------------------------------------------------ #
What I Learned
How to inspect running processes
How to monitor services using systemctl
How to check logs using journalctl and tail
Basic troubleshooting workflow for Linux services

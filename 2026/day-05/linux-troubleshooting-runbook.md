Markdown

# Day 05 – Linux Troubleshooting Runbook

## Target Service / Process
Service inspected: Docker

Reason:
Docker is a commonly used DevOps service and provides useful logs, networking, and resource usage for troubleshooting practice.

---

# 1. Environment Basics

## Command 1
        
          uname -a

##  Observation

Verified kernel version and system architecture. System is running Ubuntu Linux on x86_64.

## Command 2  -
          
           cat /etc/os-release

##  Observation

Confirmed operating system version for compatibility and troubleshooting context. 

## 2. Filesystem Sanity Check

## Command 3
          mkdir -p /tmp/runbook-demo
          cp /etc/hosts /tmp/runbook-demo/hosts-copy
          ls -l /tmp/runbook-demo

##  Observation

Filesystem is writable and file copy operations are functioning normally.

##  Command 4
          df -h

## Observation

Disk usage is healthy. Root partition has sufficient free space.

## 3. CPU & Memory Snapshot

## Command 5
          free -h

## Observation

Memory usage is normal and no swap is currently being used.

## Command 6
          ps -o pid,pcpu,pmem,comm -C dockerd

## Observation

Docker daemon is running with low CPU and moderate memory usage.

## 4. Disk & IO Checks

## Command 7
du -sh /var/log

## Observation

Log directory size is manageable. No immediate disk pressure from logs.

## Command 8
           vmstat 1 3

## Observation

No heavy IO wait observed. System appears responsive.

## 5. Network Snapshot

## Command 9
          ss -tulpn

## Observation

Docker-related ports are listening correctly.

## Command 10
          curl -I http://localhost

## Observation

Local web service is reachable and responding successfully.

## 6. Logs Reviewed

## Command 11
           journalctl -u docker -n 50

## Observation

No recent critical errors found in Docker service logs.

## Command 12
           tail -n 50 /var/log/syslog

## Observation

System logs show normal Docker startup activity without failures.

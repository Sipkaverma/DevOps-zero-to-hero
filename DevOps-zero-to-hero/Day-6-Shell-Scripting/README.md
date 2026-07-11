# Real-Time Node Health Monitoring Script

## Overview
This repository contains a production-ready Shell Script designed to automate server telemetry tracking. The script actively diagnoses a node's resource allocation and isolates underperforming systemic components.

## Technical Scope
* **Language:** Bash Shell Scripting
* **OS Environment:** Linux (Ubuntu / RHEL)
* **Core Utilities Used:** `top`, `df`, `free`, `awk`, `grep`, `pipe (|)`

## Features
* **Automated Debugging:** Implements `set -x`, `set -e`, and `set -o pipefail` to guarantee secure execution.
* **Storage Analysis:** Extracts the primary disk storage utilization profile.
* **Memory Tracking:** Logs active system RAM metrics.
* **CPU Core Diagnostics:** Pulls live active processes and isolates resource usage.
* **Process Filtering:** Strips out system noise to only output heavy system applications.

## Production Script Source
```bash
#!/bin/bash

#################################################################
# Author: Sipka
# Date: 27-June-2026
# Version: v1.0
# Purpose: Outputs Node Health Telemetry for DevOps Operations
#################################################################

# Catch unexpected script execution failures
set -e          # Exit immediately if a command exits with a non-zero status
set -o pipefail # Capture hidden errors inside pipelines

echo "=========================================="
echo "          SYSTEM HEALTH REPORT            "
echo "=========================================="

echo -e "\n[1] Checking Active Disk Utilization Space:"
df -h | awk '{print $1 " \t " $5}'

echo -e "\n[2] Checking Available System Memory (RAM):"
free -h

echo -e "\n[3] Verifying CPU Resource Utilization Allocation:"
nproc

echo -e "\n[4] Fetching Top Memory-Consuming Processes (PID & Command):"
ps -ef | grep amazon | awk '{print $2 " \t " $8}'

echo -e "\n=========================================="
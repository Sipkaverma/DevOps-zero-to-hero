# Day 15: Configuration Management & Automation with Ansible

## Overview
This repository documents the hands-on implementation of Configuration Management using **Ansible**. The objective was to eliminate manual server provisioning by automating package installation, configuration files, and service management using declarative YAML Playbooks across multi-node environments.

---

## 🛠️ Architecture & Core Mechanics

Ansible operates using an **Agentless Architecture**, leveraging standard **SSH (Port 22)** for Linux nodes.

+----------------------------+
   |   Ansible Control Node     |
   |  (Or GitHub Runner Node)   |
   +--------------+-------------+
                  |
                  | Push via SSH (Key Authentication)
                  |
    +-------------+-------------+
    |                           |
    v                           v
+---------------+           +---------------+
| Target Server |           | Target Server |
|   (Web Node)  |           |   (DB Node)   |
+---------------+           +---------------+

### Key Components Built:
1. **Inventory (`hosts.ini`):** Defines managed nodes, grouping target hosts logically (e.g., `[webservers]`, `[dbservers]`).
2. **Ansible Configuration (`ansible.cfg`):** Configures default inventory paths, remote user settings, and SSH host key validation controls.
3. **Playbooks (`playbook.yml`):** Declarative YAML scripts defining tasks, handlers, and idempotent state execution.

---

## 🚀 Execution Workflow & Real Debugging Logs

### 1. Verification & Ad-Hoc Execution
Tested connectivity and system stats across target infrastructure using ad-hoc modules:

# Test connectivity across all managed inventory nodes
ansible all -m ping -i hosts.ini

# Check disk usage across web nodes
ansible webservers -m command -a "df -h" -i hosts.ini

### 2. Idempotent Playbook Deployment
Executed end-to-end web server environment setup:
ansible-playbook -i hosts.ini deploy-app.yml --check # Dry run
ansible-playbook -i hosts.ini deploy-app.yml         # Live Execution


### 🔧 Real-World Debugging & Lessons Learned
During the execution, we faced and resolved key production scenarios:

1. SSH Host Key Checking Interruption:

Issue: Automated CI/CD execution stalled waiting for SSH key confirmation prompt (Host key verification failed).

Fix: Configured host_key_checking = False inside ansible.cfg for controlled deployment environments.

2. Sudo Elevation Errors (Permission Denied):

Issue: Package installation failed when running as non-root user.

Fix: Enforced explicit task-level privilege escalation using become: yes in Ansible playbooks.

### Implemetations
![Ansible-playbook](<WhatsApp Image 2026-07-17 at 1.56.39 PM.jpeg>)
![Ansible-adhoc command](<WhatsApp Image 2026-07-17 at 1.56.39 PM-1.jpeg>)
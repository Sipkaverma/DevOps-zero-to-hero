# 🚀 DevOps: Zero to Hero Journey

Welcome to my DevOps learning repository! This project tracks my hands-on journey through the "DevOps Zero to Hero" playlist. Instead of just watching videos, I am focusing on **building in public**, breaking infrastructure, and documenting real-world troubleshooting.

---

## 🛠️ Current Tech Stack & Tools
* **Operating System / Scripting:** Linux CLI, Shell Scripting Basics
* **Version Control:** Git & GitHub (Branching, Merge Conflict Resolution)
* **Cloud Infrastructure:** AWS (EC2, IAM, S3, Security Groups)
* **Configuration Management:** Ansible *(Up Next!)*

---

## 📈 Learning Progress & Milestones

### 🔹 Module 1: The Foundations (Videos 1 - 14)
* **Status:** Complete ✅
* **Key Learnings:**
  * Mastered essential Linux systems administration and command-line operations.
  * Set up secure access patterns using AWS IAM roles and custom Security Groups.
  * Configured compute instances (AWS EC2) and deployed applications manually to understand the friction before automation.
  * Handled advanced Git troubleshooting (including resolving nested repository/submodule boundary errors).
* **Live Lab Project:** Successfully completed a manual application architecture deployment on AWS cloud infrastructure.

### 🔹 Module 2: Automation & Configuration Management
* **Status:** In Progress / Upcoming ⏳
* **Target:** Deep-diving into **Ansible** to eliminate manual server setup and automate multi-node infrastructure.

---

## 🔧 Technical Challenges & Resolution (Troubleshooting)

### 1. Git Submodule Boundary & Index Conflict
* **Issue:** Execution of `git add` blocked by an unconfigured nested repository index (`error: subfolder does not have a commit checked out`).
* **Root Cause:** A pre-existing `.git` initialization within a subfolder conflicted with the parent repository configuration.
* **Resolution:** Purged the internal subfolder `.git` state via CLI, flushed the staging index cache (`git rm --cached`), and re-indexed the tracking directory under a unified main branch structure.

---

## 📬 Connect with Me
**LinkedIn:** [https://www.linkedin.com/in/sipka-verma-669a6b2a6?utm_source=share_via&utm_content=profile&utm_medium=member_android]
**Instagram** [https://www.instagram.com/sipkaverma?igsh=MTRlY3Npc3hyaTZlYg==]
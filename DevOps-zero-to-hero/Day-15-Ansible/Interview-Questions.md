# Day 15: Ansible Core & Production Interview Questions

### Q1: What makes Ansible "Agentless", and how does it execute commands on remote nodes?
**Answer:**
Ansible does not require custom agent software or daemons running on managed nodes. Instead, it uses standard protocols:
- **Linux/Unix:** SSH (`Port 22`) using Python modules pushed to temporary directories (`/tmp`) and executed.
- **Windows:** WinRM.

Once the tasks complete, Ansible automatically cleans up the temporary Python scripts on the remote host, minimizing resource overhead and security exposure.

---

### Q2: What is "Idempotency" in Ansible, and why is it crucial for infrastructure automation?
**Answer:**
Idempotency ensures that executing a playbook multiple times produces the exact same system state without unintended side effects. 
- If a package is already installed and running at the target version, Ansible skips re-installing it (`ok` status).
- If the system state has drifted, Ansible applies changes (`changed` status) to bring it back to the desired configuration.

*Why it matters:* Prevents service interruptions, configuration drift, and duplicate resource creation during repeated pipeline runs.

---

### Q3: What is the difference between an Ad-Hoc command, a Playbook, and a Role in Ansible?
**Answer:**
- **Ad-Hoc Command:** One-line command executed for quick, non-repetitive tasks (e.g., `ansible all -m ping`).
- **Playbook:** A single YAML file containing structured tasks, handlers, and variables meant for repeatable automation.
- **Role:** A modular, reusable directory structure (containing `tasks/`, `handlers/`, `vars/`, `templates/`, `defaults/`) designed to break complex playbooks into maintainable software components.

---

### Q4: How do handlers work in Ansible Playbooks, and when are they triggered?
**Answer:**
Handlers are special tasks that execute **only when notified** by a primary task that reports a `changed` status.

*Example Scenario:* Updating an Nginx configuration template triggers a handler to restart `nginx`. If the config file remains unchanged, the restart handler is skipped, avoiding unnecessary service downtime. Handlers run once at the end of the play by default.

---

### Q5: How do you handle secrets, credentials, and sensitive parameters in Ansible?
**Answer:**
Production secrets (API keys, SSH passwords, database tokens) are handled using **Ansible Vault**:
1. Encrypt sensitive YAML variables using `ansible-vault encrypt vars/vault.yml`.
2. Decrypt or execute playbooks securely using:
   ```bash
   ansible-playbook -i hosts.ini site.yml --vault-password-file .vault_pass
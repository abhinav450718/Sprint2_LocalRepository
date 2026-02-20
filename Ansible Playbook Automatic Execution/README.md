# Ansible Playbook Automatic Execution with Inventory and Secrets Management

---

## Author Information

| Author           | Created on | Version | Last updated by  | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | ---------------- | -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 20-02-2026 | v1.0    | Abhinav Sikarwar | 20-02-2026     | Aayush Verma| Shreya Jaiswal| Ashwani   |

---

## Table of Contents

1. Introduction
2. Playbook Automatic Execution Overview
3. Inventory Management
4. Secrets Management
5. Playbook Execution Workflow
6. Execution Command
7. Conclusion
8. Contact Information
9. References

---

## 1. Introduction

This document provides an overview of how Ansible playbooks are automatically executed on target systems using proper inventory and secrets management. The inventory file defines the target systems and connection details, while secrets management ensures secure authentication. Using this approach, the Ansible control node securely connects to target systems and executes playbooks automatically, ensuring consistent, reliable, and secure infrastructure configuration.

Ansible is an open-source automation tool used for configuration management and infrastructure deployment. It enables automated execution of predefined tasks on remote systems using playbooks, without requiring agents on target machines.

---

## 2. Playbook Automatic Execution Overview

Automatic execution of an Ansible playbook is the process where the Ansible control node executes predefined automation tasks on target systems defined in the inventory file.

This process includes:

* Identifying target systems using inventory
* Loading secure authentication secrets
* Establishing secure SSH connection
* Executing playbook tasks on target systems
* Applying configuration automatically

This ensures consistent and automated system configuration.

---

## 3. Inventory Management

The inventory file defines the list of target systems where the playbook will be executed.

### Example Inventory File

```ini
[web]
web-server ansible_host=10.0.1.10 ansible_user=ubuntu

[database]
db-server ansible_host=10.0.2.10 ansible_user=ubuntu
```

### Purpose of Inventory

| Component          | Description                                    |
| ------------------ | ---------------------------------------------- |
| Host definition    | Specifies target system hostname or IP address |
| Host grouping      | Organizes systems based on roles               |
| Connection details | Defines SSH user and access details            |

The inventory ensures that playbooks execute on the correct target systems.

---

## 4. Secrets Management

Secrets management ensures secure authentication when connecting to target systems.

Ansible uses secure authentication methods such as SSH private keys or encrypted secrets using Ansible Vault.

### Example Secret Configuration

```yaml
ansible_ssh_private_key_file: /secure/path/private-key.pem
```

### Purpose of Secrets Management

| Secret Type       | Description                                       |
| ----------------- | ------------------------------------------------- |
| SSH Private Key   | Authenticates secure connection to target systems |
| Encrypted Secrets | Protects sensitive authentication information     |

Secrets are securely used during execution without exposing sensitive information.

---

## 5. Playbook Execution Workflow

The following workflow describes how the playbook is automatically executed on target systems:

<img width="465" height="419" alt="image" src="https://github.com/user-attachments/assets/4799f40c-1846-4981-8b58-f5c705a22ee5" />

This workflow ensures secure and automated configuration of infrastructure.

---

## 6. Execution Command

The playbook is executed using the following command:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

### Command Explanation

| Parameter        | Description                                            |
| ---------------- | ------------------------------------------------------ |
| ansible-playbook | Executes the playbook                                  |
| -i inventory.ini | Specifies the inventory file containing target systems |
| playbook.yml     | Defines the automation tasks                           |

This command connects to target systems and executes the playbook automatically.

---

## 7. Conclusion

Ansible playbook automatic execution enables secure and consistent configuration of target systems. The inventory file defines the target systems, and secrets management ensures secure authentication. The Ansible control node uses this information to establish secure connections and execute playbooks automatically, ensuring reliable and automated infrastructure management.

---

## 8. Contact Information

| Name             | Email                              |
| ---------------- | ---------------------------------- |
| Abhinav Sikarwar | abhinav.sikarwar@mygurukulam.co    |

---

## 9. References

| Reference               | Description                                 |
| ----------------------- | ------------------------------------------- |
| Ansible Documentation CI| [Ansible Documentation CI](https://faisalakhan98.atlassian.net/browse/SCRUM-51) |
| Ansible Documentation CD| [Ansible Documentation CD](https://faisalakhan98.atlassian.net/browse/SCRUM-52) |


---

# Ansible Playbook Execution Documentation (Continuous Deployment - CD)

<img width="1000" height="420" alt="image" src="https://github.com/user-attachments/assets/a2722d32-295f-4c24-9691-4956045a8fb1" />

---

## Author Information

| Author           | Created on | Version | Last Edited On | L0 Reviewer  | L1 Reviewer    | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ------------ | -------------- | ----------- |
| Abhinav Sikarwar | 20-02-2026 | v2.0   | 20-02-2026     | Aayush Verma | Shreya Jaiswal | Ashwani     |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Benefits of Ansible in CD](#2-benefits-of-ansible-in-cd)
3. [Playbook Automatic Execution Overview](#3-playbook-automatic-execution-overview)
4. [Inventory Management](#4-inventory-management)
5. [Secrets Management](#5-secrets-management)
6. [Playbook Execution Workflow (CD Flow)](#6-playbook-execution-workflow-cd-flow)
7. [Execution Command](#7-execution-command)
8. [Troubleshooting](#8-troubleshooting)
9. [Conclusion](#9-conclusion)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

## 1. Introduction

This document explains how **Ansible Playbooks are used in Continuous Deployment (CD)** to automate infrastructure configuration and application deployment.

In a DevOps pipeline:

* **CI (Continuous Integration)** handles build, testing, and validation
* **CD (Continuous Deployment)** handles automated deployment

Ansible is used in the CD stage to:

* Deploy applications
* Configure infrastructure
* Ensure consistency across environments

This enables **automated, reliable, and repeatable deployments**.

---

## 2. Benefits of Ansible in CD

* Automation reduces manual errors
* Faster and consistent deployments
* Works across multiple servers simultaneously
* Easily integrates with CI/CD tools (Jenkins, GitLab CI)
* Agentless architecture (no installation on target nodes)
* Scalable for cloud and dynamic environments

---

## 3. Playbook Automatic Execution Overview

In CD pipelines, Ansible playbooks are executed automatically after successful CI stages.

This process includes:

* Pipeline trigger after code merge
* Target system identification using inventory
* Secure secrets loading
* SSH connection establishment
* Execution of playbook tasks
* Deployment of application/configuration

This ensures **continuous deployment with minimal manual intervention**.

---

## 4. Inventory Management

Inventory defines **where the deployment will happen** (dev, staging, production).

### Static Inventory

Static inventory is a manually defined file that lists the target systems.

### Example Static Inventory File
```ini
[web]
web-server ansible_host=10.0.1.10 ansible_user=ubuntu

[database]
db-server ansible_host=10.0.2.10 ansible_user=ubuntu
```
### Purpose of Static Inventory

| Component          | Description                                    |
| ------------------ | ---------------------------------------------- |
| Host definition    | Specifies target system hostname or IP address |
| Host grouping      | Organizes systems based on roles               |
| Connection details | Defines SSH user and access details            |

Static inventory is simple and easy to manage when the infrastructure environment is small and stable.

---

### Dynamic Inventory

Dynamic inventory automatically retrieves the list of target systems from external sources such as cloud providers, APIs, or configuration databases.

Instead of manually updating inventory files, Ansible dynamically queries infrastructure platforms like AWS, Azure, or Kubernetes to obtain the latest list of hosts.

### Example Dynamic Inventory (AWS)

```bash
aws ec2 describe-instances
```

Example Ansible command using dynamic inventory:

```bash
ansible-playbook -i aws_ec2.yml playbook.yml
```

### Example Dynamic Inventory Configuration

```yaml
plugin: aws_ec2
regions:
  - us-east-1
keyed_groups:
  - key: tags.Name
```

### Purpose of Dynamic Inventory

| Feature                  | Description                               |
| ------------------------ | ----------------------------------------- |
| Automatic host discovery | Fetches servers dynamically               |
| Cloud integration        | Works with AWS, Azure, GCP                |
| Real-time updates        | Reflects infrastructure changes instantly |
| Scalability              | Suitable for large environments           |

Dynamic inventory eliminates the need to manually update host lists.

---

### Best Practice

* Use **dynamic inventory** in CD pipelines
* Use **static inventory** for small or fixed environments

---

## 5. Secrets Management

Secrets are required for secure deployment.
Ansible uses secure authentication methods such as SSH private keys or encrypted secrets using Ansible Vault.

Example:

```yaml
ansible_ssh_private_key_file: /secure/path/private-key.pem
```

Used for:

* SSH authentication
* Protecting sensitive data

In CD pipelines, secrets are managed using:

* Jenkins Credentials
* GitLab Secrets
* AWS Secrets Manager

---

## 6. Playbook Execution Workflow (CD Flow)

<img width="556" height="680" alt="image" src="https://github.com/user-attachments/assets/61f5385e-2fff-4a8d-a972-3ed635e4bc4c" />

### Step-by-Step CD Flow

1. **Code Update**
   Developer updates Ansible playbook and pushes to repository

2. **Pull Request & Review**
   Code is validated and reviewed

3. **Merge to Main Branch**
   Approved changes are merged

4. **Pipeline Trigger**
   CI/CD pipeline starts automatically

5. **Secrets & Inventory Initialization**

   * Secrets are securely loaded
   * Inventory is fetched (static/dynamic)

6. **Playbook Execution**
   Ansible executes playbook on target servers

7. **Deployment Completed**
   Application/configuration is deployed successfully

---

## 7. Execution Command

```bash
ansible-playbook -i inventory.ini playbook.yml
```

In CD pipelines, this command is executed automatically by tools like Jenkins.

---

## 8. Troubleshooting

| Issue                 | Cause           | Fix                    |
| --------------------- | --------------- | ---------------------- |
| SSH connection failed | Wrong IP/key    | Verify inventory & key |
| Hosts unreachable     | Inventory issue | Check format           |
| Playbook error        | YAML issue      | Run syntax check       |
| CD not triggered      | CI failed       | Check pipeline logs    |

---

## 9. Conclusion

Ansible Playbooks play a crucial role in **Continuous Deployment (CD)** by enabling:

* Automated deployments
* Consistent infrastructure configuration
* Reduced manual errors
* Faster release cycles

When integrated with CI/CD pipelines, Ansible ensures **end-to-end automation from code commit to deployment**.

---

## 10. Contact Information

| Name             | Email                                                                     |
| ---------------- | ------------------------------------------------------------------------- |
| Abhinav Sikarwar | [abhinav.sikarwar@mygurukulam.co](mailto:abhinav.sikarwar@mygurukulam.co) |

---

## 11. References

| Reference                | Description                                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Ansible Documentation CI | [https://faisalakhan98.atlassian.net/browse/SCRUM-51](https://faisalakhan98.atlassian.net/browse/SCRUM-51) |
| Ansible Documentation CD | [https://faisalakhan98.atlassian.net/browse/SCRUM-52](https://faisalakhan98.atlassian.net/browse/SCRUM-52) |

---


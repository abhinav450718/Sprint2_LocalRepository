# Proof of Concept (POC): Dependency Scanning using "Trivy"

---

## Author Information

| Author           | Created on | Version | Last Edited On | L0 Reviewer  | L1 Reviewer    | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ------------ | -------------- | ----------- |
| Abhinav Sikarwar | 25-02-2026 | v1.0    | 25-02-2026     | Aayush Verma | Shreya Jaiswal | Ashwani     |

---

# Table of Contents

1. [Objective](#1-objective)
2. [Environment Details](#2-environment-details)
3. [Step 1: Install Trivy](#3-step-1-install-trivy)
4. [Step 2: Verify Trivy Installation](#4-step-2-verify-trivy-installation)
5. [Step 3: Create Project Directory](#5-step-3-create-project-directory)
6. [Step 4: Create Vulnerable requirements.txt](#6-step-4-create-vulnerable-requirementstxt)
7. [Step 5: Perform Dependency Scan using Trivy](#7-step-5-perform-dependency-scan-using-trivy)
8. [Step 6: View Vulnerability Output in Table Format](#8-step-6-view-vulnerability-output-in-table-format)
9. [Step 7: Generate Dependency Scan Report File](#9-step-7-generate-dependency-scan-report-file)
10. [Step 8: Fix Vulnerabilities using Corrected requirements.txt](#10-step-8-fix-vulnerabilities-using-corrected-requirementstxt)
11. [Step 9: Re-scan Dependencies after Fix](#11-step-9-re-scan-dependencies-after-fix)
12. [Step 10: CI Integration Command](#12-step-10-ci-integration-command)
13. [What Happens Internally](#13-what-happens-internally)
14. [Dependency Scanning Workflow Diagram](#14-dependency-scanning-workflow-diagram)
15. [Result](#15-result)
16. [Conclusion](#16-conclusion)

---

# 1. Objective

The objective of this POC is to demonstrate how dependency vulnerability scanning can be performed using Trivy to identify security vulnerabilities in Python Attendance and Notification service dependencies.

This ensures vulnerable third-party libraries are detected and fixed before deployment, improving overall application security.

---

# 2. Environment Details

| Component        | Value                                |
| ---------------- | ------------------------------------ |
| Operating System | Ubuntu Linux                         |
| Language         | Python 3                             |
| Tool             | Trivy                                |
| Scan Type        | Dependency Vulnerability Scanning    |
| Dependency File  | requirements.txt                     |
| Scan Target      | Attendance and Notification Services |

---

# 3. Step 1: Install Trivy

Install Trivy using snap:

```bash
sudo snap install trivy
```

Output:

```
trivy installed successfully
```
<img width="924" height="114" alt="image" src="https://github.com/user-attachments/assets/0b9eaaea-8ec8-4df9-ba39-d8a058e8b520" />

---

# 4. Step 2: Verify Trivy Installation

Verify installation:

```bash
trivy --version
```

Output:

```
Version: 0.52.2
```
<img width="1600" height="247" alt="image" src="https://github.com/user-attachments/assets/dfcf52a0-f20b-4bc0-a798-2df90b93c6ef" />

This confirms Trivy is installed successfully.

---

# 5. Step 3: Create Project Directory

Create project directory:

```bash
mkdir python_DS
cd python_DS
```

# 6. Step 4: Create Vulnerable requirements.txt

Create dependency file:

```bash
nano requirements.txt
```

Paste vulnerable dependencies:

<img width="954" height="420" alt="image" src="https://github.com/user-attachments/assets/26d51e80-d79f-4d23-8c15-3d310a845b04" />


Save file.

Verify file:

```bash
ls
```

Output:

```
requirements.txt
```

---

# 7. Step 5: Perform Dependency Scan using Trivy

Run dependency scan:

```bash
trivy fs .
```
<img width="1600" height="247" alt="image" src="https://github.com/user-attachments/assets/4d1f93d5-0a00-4855-af03-31a45c952db3" />

Trivy performs vulnerability scanning on dependencies.

---

# 8. Step 6: View Vulnerability Output in Table Format

Run scan with table output:

```bash
trivy fs --scanners vuln --format table .
```

Output shows:

* Library name
* Vulnerability ID
* Severity
* Installed version
* Fixed version

Example:

```
Flask     HIGH       1.0.2    Fixed: 2.3.3
requests  HIGH       2.19.1   Fixed: 2.31.0
celery    CRITICAL   4.2.0    Fixed: 5.3.4
```
<img width="1193" height="1012" alt="image" src="https://github.com/user-attachments/assets/d962296a-413d-4a0c-a412-7582ad359e1a" />

This confirms vulnerable dependencies.

---

# 9. Step 7: Generate Dependency Scan Report File

Generate report file:

```bash
trivy fs --scanners vuln --format table -o trivy-report.txt .
```

View report:

```bash
cat trivy-report.txt
```
<img width="1543" height="121" alt="image" src="https://github.com/user-attachments/assets/8ccaaa1d-2d9d-4ea6-8627-cebddd02e9d9" />
<img width="1103" height="1014" alt="image" src="https://github.com/user-attachments/assets/7a3d8bd1-a56e-45f8-8089-eea77d436b8c" />

Report contains vulnerability details.

Run this command to enforce security in CI pipeline:

```bash
trivy fs --scanners vuln --exit-code 1 --severity HIGH,CRITICAL .
```
<img width="1554" height="954" alt="image" src="https://github.com/user-attachments/assets/74fc843d-8b15-45d7-8ab4-389498615bf6" />

---

# 10. Step 8: Fix Vulnerabilities using Corrected requirements.txt


Create project directory:

```bash
mkdir python_DS1
cd python_DS1
```
Update dependency file:

```bash
nano requirements1.txt
```

Replace with secure dependencies:

<img width="1045" height="269" alt="image" src="https://github.com/user-attachments/assets/d6208254-d1fd-4f0b-93c1-8b8dfde40a4a" />


Save file.

---

# 11. Step 9: Re-scan Dependencies after Fix

Run scan again:

```bash
trivy fs --scanners vuln  .
```
<img width="1600" height="178" alt="image" src="https://github.com/user-attachments/assets/d73e060a-784c-485d-8e89-0d822cdd3a7e" />

Output shows reduced or no vulnerabilities.

This confirms vulnerabilities are fixed.

---

# 12. Step 10: CI Integration Command

Run this command to enforce security in CI pipeline:

```bash
trivy fs --scanners vuln --exit-code 1 --severity HIGH,CRITICAL .
```
<img width="1378" height="101" alt="image" src="https://github.com/user-attachments/assets/ba6fbc0a-b418-45f7-b05c-1bcbaed9d12a" />

Behavior:

* If vulnerabilities exist → CI fails
* If no vulnerabilities → CI passes

This prevents insecure deployments.

---

# 13. What Happens Internally

Trivy performs the following steps:

1. Reads requirements.txt
2. Identifies dependency versions
3. Compares versions with vulnerability database
4. Detects known vulnerabilities (CVEs)
5. Displays vulnerability details
6. Suggests fixed versions
7. Generates security report

This ensures dependency security.

---

# 14. Dependency Scanning Workflow Diagram

<img width="586" height="369" alt="image" src="https://github.com/user-attachments/assets/51282f7b-b938-4947-b44f-19efcc646b9c" />


---

# 15. Result

Trivy successfully detected vulnerabilities in Attendance and Notification service dependencies.

Generated report contains:

* Vulnerable library name
* Severity level
* CVE ID
* Fixed version

After updating dependencies, vulnerabilities were resolved.

This confirms successful dependency scanning implementation.

---

# 16. Conclusion

This POC demonstrates how Trivy can be used to perform dependency vulnerability scanning on Python Attendance and Notification services.

Trivy successfully identified vulnerable dependencies, generated detailed vulnerability reports, and helped remediate security risks by upgrading dependencies.

Dependency scanning is essential for secure CI/CD pipelines because it prevents insecure libraries from being deployed into production.

Trivy is recommended due to its open-source nature, fast scanning speed, ease of integration, and CI/CD compatibility.

---

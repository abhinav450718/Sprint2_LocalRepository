# Proof of Concept (POC): DAST using "OWASP ZAP"

---

## Author Information

| Author           | Created on | Version | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 25-02-2026 | v1.0    | 25-02-2026     | Aayush Verma| Shreya Jaiswal| Ashwani  |

---

## Table of Contents

1. [Objective](#1-objective)
2. [Environment Details](#2-environment-details)
3. [Step 1: Download OWASP ZAP](#3-step-1-download-owasp-zap)
4. [Step 2: Extract OWASP ZAP](#4-step-2-extract-owasp-zap)
5. [Step 3: Start OWASP ZAP](#5-step-3-start-owasp-zap)
6. [Step 4: Create Python Attendance and Notification Application](#6-step-4-create-python-attendance-and-notification-application)
7. [Step 5: Install Flask](#7-step-5-install-flask)
8. [Step 6: Run Python Application](#8-step-6-run-python-application)
9. [Step 7: Perform DAST Scan using OWASP ZAP](#9-step-7-perform-dast-scan-using-owasp-zap)
10. [Step 8: Vulnerability Detection](#10-step-8-vulnerability-detection)
11. [Step 9: Generate DAST Security Report](#11-step-9-generate-dast-security-report)
12. [Step 10: View Security Report](#12-step-10-view-security-report)
13. [What Happens Internally](#13-what-happens-internally)
14. [DAST Workflow Diagram](#14-dast-workflow-diagram)
15. [Result](#15-result)
16. [Conclusion](#16-conclusion)

---

# 1. Objective

The objective of this POC is to demonstrate how Dynamic Application Security Testing (DAST) can be performed using OWASP ZAP to identify runtime security vulnerabilities in a Python-based Attendance and Notification application.

---

# 2. Environment Details

| Component             | Value                                |
| --------------------- | ------------------------------------ |
| Operating System      | Ubuntu Linux                         |
| Language              | Python 3                             |
| Application Framework | Flask                                |
| DAST Tool             | OWASP ZAP                            |
| Scan Type             | Dynamic Application Security Testing |
| Application Port      | 5000                                 |

---

# 3. Step 1: Download OWASP ZAP

Download OWASP ZAP from official GitHub release:

```bash
wget https://github.com/zaproxy/zaproxy/releases/download/v2.16.1/ZAP_2.16.1_Linux.tar.gz
```

<img width="1600" height="560" alt="image" src="https://github.com/user-attachments/assets/7c106d18-5454-4e30-86fd-1a42f55b0c71" />

This downloads the OWASP ZAP package.

Verification:

```bash
ls
```

Output:

```
ZAP_2.16.1_Linux.tar.gz
```

---

# 4. Step 2: Extract OWASP ZAP

Extract the downloaded file:

```bash
tar -xvf ZAP_2.16.1_Linux.tar.gz
```

<img width="1488" height="1010" alt="image" src="https://github.com/user-attachments/assets/e884d980-b8b8-40a4-95c3-aa85bbc97dbe" />

Move into directory:

```bash
cd ZAP_2.16.1
```

Verify files:

```bash
ls
```

Output:

```
zap.sh
zap.jar
lib/
plugin/
```

---

# 5. Step 3: Start OWASP ZAP

Run OWASP ZAP:

```bash
./zap.sh
```

<img width="1600" height="853" alt="image" src="https://github.com/user-attachments/assets/1eebf3d7-7a6d-452a-a12d-c9f58c381fc1" />
<img width="1600" height="848" alt="image" src="https://github.com/user-attachments/assets/05057e2a-2e23-4f64-afd4-a76b37d7f720" />

OWASP ZAP GUI opens successfully.

This tool will perform dynamic security scanning.

---

# 6. Step 4: Create Python Attendance and Notification Application

Create application file:

```bash
nano attendance_app.py
```

Paste the following code:

![WhatsApp Image 2026-02-25 at 2 29 58 PM](https://github.com/user-attachments/assets/5b042411-cfc3-49b8-a0c2-c7e162fe6b69)

Save file.

This application contains intentionally vulnerable endpoints.

---

# 7. Step 5: Install Flask

Install Flask:

```bash
sudo apt install python3-flask
```

<img width="1393" height="958" alt="image" src="https://github.com/user-attachments/assets/a095f8fd-3e72-44bc-8ef8-8fc99aa7080e" />

---

# 8. Step 6: Run Python Application

Start the application:

```bash
python attendance_app.py
```

Output:

```
Running on http://127.0.0.1:5000
```

<img width="1570" height="955" alt="image" src="https://github.com/user-attachments/assets/d44fcebb-2e85-4a5e-8b10-2432734217d3" />

The application is now live and ready for security scanning.

---

# 9. Step 7: Perform DAST Scan using OWASP ZAP

Open OWASP ZAP GUI.

Go to:

```
Quick Start Tab
```

Enter target URL:

```
http://127.0.0.1:5000
```

Click:

```
Attack
```

<img width="1600" height="846" alt="image" src="https://github.com/user-attachments/assets/0e9e0ead-858e-4356-8102-6c2fce28dcc8" />

OWASP ZAP performs the following actions:

* Spider Scan → discovers endpoints
* Passive Scan → analyzes responses
* Active Scan → sends attack payloads

---

# 10. Step 8: Vulnerability Detection

OWASP ZAP detects vulnerabilities such as:

* Missing Security Headers
* Input validation issues
* Information disclosure
* Potential Cross-Site Scripting (XSS)

All vulnerabilities appear under:

```
Alerts Tab
```

<img width="1600" height="319" alt="image" src="https://github.com/user-attachments/assets/e681e1aa-4683-46ef-82b5-cce03266e33f" />

Each vulnerability includes:

* Risk level
* Description
* Affected URL
* Recommended fix

---

# 11. Step 9: Generate DAST Security Report

In OWASP ZAP:

Click:

```
Report → Generate Report
```

Select:

```
HTML Report
```

Save file as:

```
2026-02-25-ZAP-Report-.html
```

<img width="1600" height="845" alt="image" src="https://github.com/user-attachments/assets/7e04b6fa-6496-41ec-a79b-abc5fbc6f120" />

Report is successfully generated.

---

# 12. Step 10: View Security Report

Copy report to Downloads folder:

```bash
cp "2026-02-25-ZAP-Report-.html" /mnt/c/Users/lenovo/Downloads/
```

<img width="365" height="150" alt="image" src="https://github.com/user-attachments/assets/21c369b4-cfbd-40fd-adb9-430717da38b2" />
<img width="1046" height="258" alt="image" src="https://github.com/user-attachments/assets/a7fcb146-8e2c-41b0-bb55-6205171f5500" />

Open Downloads folder in Windows.

Double-click:

```
2026-02-25-ZAP-Report-.html
```

<img width="1600" height="713" alt="image" src="https://github.com/user-attachments/assets/f3fb1d24-9629-44a9-876a-89ec686539ce" />
<img width="1600" height="433" alt="image" src="https://github.com/user-attachments/assets/4713b1d3-1fbe-4d5d-918e-048b6faabf6a" />

Report opens in browser.

The report contains:

* Executive Summary
* Risk Summary
* Vulnerability Details
* Affected URLs
* Remediation Recommendations

---

# 13. What Happens Internally

OWASP ZAP performs the following:

1. Connects to running application
2. Discovers application endpoints
3. Sends malicious test payloads
4. Analyzes responses
5. Identifies vulnerabilities
6. Generates detailed security report

This simulates real attacker behavior.

---

# 14. DAST Workflow Diagram

<img width="648" height="537" alt="image" src="https://github.com/user-attachments/assets/857b6e95-a4ac-46db-b3b1-786462da9ba5" />

---

# 15. Result

OWASP ZAP successfully identified vulnerabilities in the Python Attendance and Notification application.

Generated report contains:

* Vulnerability name
* Risk level
* Description
* Solution recommendation

This confirms successful DAST implementation.

---

# 16. Conclusion

This POC demonstrates how OWASP ZAP can be used to perform Dynamic Application Security Testing on a Python-based application. OWASP ZAP successfully scanned the running Attendance and Notification application, identified runtime vulnerabilities, and generated a detailed security report.

DAST helps detect exploitable vulnerabilities before deployment and is essential for secure CI/CD pipelines.

OWASP ZAP is recommended due to its open-source nature, ease of use, automation support, and CI/CD integration capabilities.

---

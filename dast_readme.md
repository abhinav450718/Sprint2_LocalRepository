# Python DAST – OWASP ZAP "Security Scan for OT Microservices"

---

## Author Information

| Author           | Created on | Version | Last edited on | L0 Reviewer  | L1 Reviewer    | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ------------ | -------------- | ----------- |
| Abhinav Sikarwar | 08-03-2026 | v1.0    | 09-03-2026     | Aayush Verma | Shreya Jaiswal | Ashwani     |

---

# Table of Contents

1. [Purpose](#purpose)
2. [Architecture Overview](#architecture-overview)
3. [DAST Scan Flow](#dast-scan-flow)
4. [Prerequisites](#prerequisites)
5. [Implementation Steps](#implementation-steps)
6. [ZAP Dynamic Analysis Report](#zap-dynamic-analysis-report)
7. [Key Findings](#key-findings)
8. [Notification API Implementation Steps](#notification-api-implementation-steps)
9. [Notification API ZAP Dynamic Analysis Report](#notification-api-zap-dynamic-analysis-report)
10. [Notification API Key Findings](#notification-api-key-findings)
11. [Combined Security Summary](#combined-security-summary)
12. [Final Conclusion](#final-conclusion)

---

# Purpose

The objective of this Proof of Concept (POC) is to perform **Dynamic Application Security Testing (DAST)** on Python-based microservices using **OWASP ZAP**.

Dynamic testing analyzes applications **while they are running** and simulates real-world attacks against exposed endpoints. This approach helps identify vulnerabilities that may not be detected through static code analysis.

The goal of this assessment is to evaluate the runtime security posture of the following services:

* **Attendance API**
* **Notification API**

The scan focuses on detecting security issues such as:

* Cross Site Scripting (XSS)
* SQL Injection
* Security misconfiguration
* Information disclosure
* Missing security headers

By performing DAST scans before deployment, organizations can **reduce production security risks and strengthen application security.**

---

# Architecture Overview

The security scan is executed in a controlled infrastructure environment where the APIs are hosted on a backend server and accessed via a bastion host.

<img width="740" height="499" alt="image" src="https://github.com/user-attachments/assets/911b3a9f-514d-4fe2-b9e8-36879b17baf1" />

### Components

| Component        | Description                            |
| ---------------- | -------------------------------------- |
| Attendance API   | Python-based microservice under test   |
| Notification API | Python-based notification microservice |
| Bastion Server   | Secure access gateway                  |
| Backend Server   | Private server hosting APIs            |
| OWASP ZAP        | Dynamic security scanning tool         |

---

# DAST Scan Flow

The Dynamic Application Security Testing workflow follows the process below.

<img width="594" height="491" alt="image" src="https://github.com/user-attachments/assets/f2a1d27b-5bc2-4273-b979-c3bacc87abe1" />

### Scan Workflow Explanation

| Stage                  | Description                                        |
| ---------------------- | -------------------------------------------------- |
| Application Deployment | API services are started locally                   |
| Spider Scan            | ZAP crawls the application and discovers endpoints |
| Active Scan            | Attack payloads are sent to detect vulnerabilities |
| Analysis               | Security alerts are generated                      |
| Report Generation      | ZAP produces detailed HTML reports                 |

---

# Prerequisites

| Tool           | Purpose                |
| -------------- | ---------------------- |
| Ubuntu EC2     | Execution environment  |
| Python 3       | Runtime for APIs       |
| OWASP ZAP      | Security scanning tool |
| Bastion Server | Secure network access  |
| SCP            | Secure report transfer |

---

# Implementation Steps

## Clone Attendance API Repository

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api
```

---

## Check Python Version

```bash
python3 --version
```

<img width="1175" height="962" alt="image" src="https://github.com/user-attachments/assets/6fa00a31-9387-4701-bf14-98cf9a842a87" />

---

## Install OWASP ZAP

```bash
wget https://github.com/zaproxy/zaproxy/releases/download/v2.17.0/ZAP_2_17_0_unix.sh
chmod +x ZAP_2_17_0_unix.sh
./ZAP_2_17_0_unix.sh
```

Verify installation

```bash
zap.sh -version
```

<img width="1600" height="749" alt="image" src="https://github.com/user-attachments/assets/60665fe1-13a4-41f8-9e0a-827d8fada6ea" />

---

## Start ZAP in Daemon Mode

```bash
sudo /opt/zaproxy/zap.sh -daemon -port 8090 -host 0.0.0.0 -config api.key=attendancekey
```

This allows scanning through the ZAP API.

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/08ed8ebf-ab0d-4e2e-8acc-63ff6b8f4281" />

---

## Run Spider Scan

```bash
curl "http://localhost:8090/JSON/spider/action/scan/?url=http://localhost:5000/&apikey=attendancekey"
```

<img width="1600" height="88" alt="image" src="https://github.com/user-attachments/assets/f5aafdf4-1d4b-4ad5-a0d7-75c2bedaffd6" />

---

## Run Active Scan

```bash
curl "http://localhost:8090/JSON/ascan/action/scan/?url=http://localhost:5000/&apikey=attendancekey"
```

<img width="1600" height="49" alt="image" src="https://github.com/user-attachments/assets/8b20951f-9521-4cc4-9c2c-0a1be834bef3" />

---

## Generate HTML Report

```bash
curl "http://localhost:8090/OTHER/core/other/htmlreport/?apikey=attendancekey" -o zap_attendance_report.html
```

<img width="1600" height="120" alt="image" src="https://github.com/user-attachments/assets/9eba9b2f-d977-40b9-b59c-266e606e8283" />

---

# ZAP Dynamic Analysis Report

### Site Scanned

```
URL: http://localhost:5000
ZAP Version: 2.17.0
Generated On: 08 Mar 2026
```

<img width="1600" height="560" alt="image" src="https://github.com/user-attachments/assets/2d6be296-f5a5-46f2-925e-9e6e61c83cb9" />
<img width="1600" height="746" alt="image" src="https://github.com/user-attachments/assets/e2f3adc5-ae3a-4494-b523-7e946595e280" />
<img width="1600" height="195" alt="image" src="https://github.com/user-attachments/assets/6b8e94b8-6ac0-4954-864b-73a14443b7fa" />
<img width="1600" height="854" alt="image" src="https://github.com/user-attachments/assets/fd7201da-7f42-4ff4-bd61-53a55a978693" />
<img width="1600" height="749" alt="image" src="https://github.com/user-attachments/assets/c1156e09-c588-42d2-b215-e4b1c3eb8385" />

---

# Key Findings

| Risk Level | Alerts |
| ---------- | ------ |
| High       | 0      |
| Medium     | 1      |
| Low        | 1      |

### Medium Severity

Content Security Policy Header not set.

Recommended Fix

```
Content-Security-Policy: default-src 'self'
```

### Low Severity

Server version disclosure detected.

Example

```
Werkzeug/3.1.6 Python/3.12.3
```

---

# Notification API Implementation Steps

## Clone Notification API

```bash
git clone https://github.com/OT-MICROSERVICES/notification-api.git
cd notification-api
```

---

## Start Notification API

```bash
python3 app.py
```

Application runs on

```
http://localhost:5001
```

---

## Start ZAP for Notification Scan

```bash
sudo /opt/zaproxy/zap.sh -daemon -port 8091 -host 0.0.0.0 -config api.key=notificationkey
```
<img width="1600" height="846" alt="image" src="https://github.com/user-attachments/assets/5f8b79a5-a83d-42d3-9dcf-d457d746e65b" />

---

## Run Spider Scan

```bash
curl "http://localhost:8091/JSON/spider/action/scan/?url=http://localhost:5001/&apikey=notificationkey"
```
<img width="934" height="139" alt="image" src="https://github.com/user-attachments/assets/32d43d54-d36f-421e-9337-2e37333a7e39" />

---

## Run Active Scan

```bash
curl "http://localhost:8091/JSON/ascan/action/scan/?url=http://localhost:5001/&apikey=notificationkey"
```
<img width="1600" height="75" alt="image" src="https://github.com/user-attachments/assets/7f3dbc05-1b0e-4005-ac2c-e390a23237d2" />

---

## Generate Security Report

```bash
curl "http://localhost:8091/OTHER/core/other/htmlreport/?apikey=notificationkey" -o zap_notification_report.html
```
<img width="1600" height="115" alt="image" src="https://github.com/user-attachments/assets/bc498969-a35a-4203-abbb-4f6388b6cc37" />

---

# Notification API ZAP Dynamic Analysis Report

### Site Scanned

```
URL: http://localhost:5001
ZAP Version: 2.17.0
```
<img width="1919" height="970" alt="image" src="https://github.com/user-attachments/assets/93fa8932-9492-4f4c-9832-8230a1b39033" />
<img width="1919" height="253" alt="image" src="https://github.com/user-attachments/assets/8c557e73-4810-4903-9a36-4340151b34f3" />
<img width="1919" height="662" alt="image" src="https://github.com/user-attachments/assets/40d91ef1-8306-4779-9513-31fc77753959" />
<img width="1899" height="690" alt="image" src="https://github.com/user-attachments/assets/d64a8b70-497c-4bfe-a856-86ef43c1206d" />

The scan analyzed all exposed endpoints of the Notification API and produced a detailed vulnerability report.

---

# Notification API Key Findings

| Risk Level | Alerts |
| ---------- | ------ |
| High       | 0      |
| Medium     | 1      |
| Low        | 1      |

### Medium Severity

Missing Content Security Policy Header.

### Low Severity

Server version disclosure.

---

# Combined Security Summary

| Microservice     | Application Port | ZAP Port | Report                       |
| ---------------- | ---------------- | -------- | ---------------------------- |
| Attendance API   | 5000             | 8090     | zap_attendance_report.html   |
| Notification API | 5001             | 8091     | zap_notification_report.html |

Both microservices were scanned independently to ensure accurate vulnerability detection.

---

# Final Conclusion

This POC demonstrates the use of **OWASP ZAP for performing Dynamic Application Security Testing on Python microservices**.

The security evaluation included:

* Attendance API
* Notification API

Key observations:

* No high-risk vulnerabilities detected
* Minor configuration issues identified
* Security headers should be implemented
* Server version disclosure should be restricted

Integrating automated DAST scans into the CI/CD pipeline can help organizations detect vulnerabilities early and strengthen application security before deployment.

---


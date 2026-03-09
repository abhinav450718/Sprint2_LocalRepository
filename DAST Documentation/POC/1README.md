# Python DAST – OWASP ZAP for Attendance API

---

## Author Information

| Author           | Created on | Version | Last edited on | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 08-03-2026 | v1.0    | 08-03-2026     | Aayush Verma|Shreya Jaiswal|Ashwani     |

---

# Table of Contents

1. [Purpose](#1-purpose)
2. [Architecture Overview](#2-architecture-overview)
3. [DAST Scan Flow](#3-dast-scan-flow)
4. [Prerequisites](#4-prerequisites)
5. [Implementation Steps](#5-implementation-steps)
6. [ZAP Dynamic Analysis Report](#6-zap-dynamic-analysis-report)
7. [Key Findings](#7-key-findings)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

# 1. Purpose

The objective of this Proof of Concept (POC) is to perform **Dynamic Application Security Testing (DAST)** on a Python-based microservice using **OWASP ZAP**.

DAST analyzes applications **while they are running** and simulates real-world attacks to identify security vulnerabilities that may occur during runtime.

This security assessment focuses on detecting vulnerabilities such as:

* Cross Site Scripting (XSS)
* SQL Injection
* Security Misconfiguration
* Information Disclosure
* Missing Security Headers

The **Attendance API** is scanned using OWASP ZAP to ensure the application meets basic security requirements before deployment.

---

# 2. Architecture Overview

The security scan was performed within a controlled environment where the application is deployed on a backend server and accessed through a bastion host.

<img width="740" height="499" alt="image" src="https://github.com/user-attachments/assets/911b3a9f-514d-4fe2-b9e8-36879b17baf1" />


### Components

| Component      | Description                          |
| -------------- | ------------------------------------ |
| Attendance API | Python-based microservice under test |
| Bastion Server | Secure access gateway                |
| Backend Server | Private server hosting the API       |
| OWASP ZAP      | Security scanning tool               |

---

# 3. DAST Scan Flow

The Dynamic Application Security Testing process follows the sequence below:

<img width="594" height="491" alt="image" src="https://github.com/user-attachments/assets/f2a1d27b-5bc2-4273-b979-c3bacc87abe1" />


### Scan Workflow Explanation

| Stage                  | Description                                     |
| ---------------------- | ----------------------------------------------- |
| Application Deployment | The Attendance API is started locally           |
| Spider Scan            | Crawls the application and discovers endpoints  |
| Active Scan            | Sends attack payloads to detect vulnerabilities |
| Analysis               | Security alerts are generated                   |
| Report Generation      | ZAP produces a detailed HTML security report    |

---

# 4. Prerequisites

| Tool           | Purpose                    |
| -------------- | -------------------------- |
| Ubuntu EC2     | Execution Environment      |
| Python 3       | Runtime for Attendance API |
| OWASP ZAP      | Security scanning tool     |
| Bastion Server | Secure network access      |
| SCP            | Secure report transfer     |

---

# 5. Implementation Steps

---

## 5.1 Clone Attendance API Repository

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api
```

---

## 5.2 Check Python Version 

```bash
python3 --version
```
<img width="1175" height="962" alt="image" src="https://github.com/user-attachments/assets/6fa00a31-9387-4701-bf14-98cf9a842a87" />

---

## 5.3 Install OWASP ZAP

```bash
wget https://github.com/zaproxy/zaproxy/releases/download/v2.17.0/ZAP_2_17_0_unix.sh
chmod +x ZAP_2_17_0_unix.sh
./ZAP_2_17_0_unix.sh
```

Verify installation:

```bash
zap.sh -version
```

<img width="1600" height="749" alt="image" src="https://github.com/user-attachments/assets/60665fe1-13a4-41f8-9e0a-827d8fada6ea" />


---

## 5.4 Start ZAP in Daemon Mode

```bash
sudo /opt/zaproxy/zap.sh -daemon -port 8090 -host 0.0.0.0 -config api.key=attendancekey
```

This enables scanning via ZAP API.

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/08ed8ebf-ab0d-4e2e-8acc-63ff6b8f4281" />
<img width="1600" height="51" alt="image" src="https://github.com/user-attachments/assets/c640b803-1769-461f-8c15-857fd91ec3e6" />


---

## 5.5 Run Spider Scan

Spider scan discovers application endpoints.

```bash
curl "http://localhost:8090/JSON/spider/action/scan/?url=http://localhost:5000/&apikey=attendancekey"
```
<img width="1600" height="88" alt="image" src="https://github.com/user-attachments/assets/f5aafdf4-1d4b-4ad5-a0d7-75c2bedaffd6" />

Check scan status:

```bash
curl "http://localhost:8090/JSON/spider/view/status/?scanId=0&apikey=attendancekey"
```

<img width="1600" height="49" alt="image" src="https://github.com/user-attachments/assets/82a4f61c-6620-4725-be72-be9f7841de97" />


---

## 5.6 Run Active Scan

Active scan simulates attacks on the discovered endpoints.

```bash
curl "http://localhost:8090/JSON/ascan/action/scan/?url=http://localhost:5000/&apikey=attendancekey"
```

<img width="1600" height="49" alt="image" src="https://github.com/user-attachments/assets/8b20951f-9521-4cc4-9c2c-0a1be834bef3" />


---

## 5.7 Generate HTML Report

```bash
curl "http://localhost:8090/OTHER/core/other/htmlreport/?apikey=attendancekey" -o zap_attendance_report.html
```

This generates the **DAST vulnerability report**.

<img width="1600" height="120" alt="image" src="https://github.com/user-attachments/assets/9eba9b2f-d977-40b9-b59c-266e606e8283" />
<img width="1264" height="86" alt="image" src="https://github.com/user-attachments/assets/703722dc-81f9-43e2-b3ef-84003703435e" />


---

# 6. ZAP Dynamic Analysis Report

### Site Scanned

```
URL: http://localhost:5000
ZAP Version: 2.17.0
Generated On: 08 Mar 2026
```

<img width="1600" height="560" alt="image" src="https://github.com/user-attachments/assets/2d6be296-f5a5-46f2-925e-9e6e61c83cb9" />

<img width="1600" height="746" alt="image" src="https://github.com/user-attachments/assets/b39de1ee-7b56-4ca7-9ce9-c880683a9ea9" />
<img width="1600" height="195" alt="image" src="https://github.com/user-attachments/assets/40c897f1-c5fb-41ef-811a-5b2a7266b077" />
<img width="1600" height="854" alt="image" src="https://github.com/user-attachments/assets/b6ce553a-da40-475e-8d07-fff28a9d31a8" />
<img width="1600" height="749" alt="image" src="https://github.com/user-attachments/assets/476a6db0-3c8c-4852-b586-1e4b0e15494d" />


---

## Alert Summary

| Risk Level    | Alerts |
| ------------- | ------ |
| High          | 0      |
| Medium        | 1      |
| Low           | 1      |
| Informational | 0      |

---

# 7. Key Findings

### Medium Severity

**Content Security Policy Header Not Set**

Content Security Policy (CSP) helps mitigate:

* Cross-Site Scripting attacks
* Data injection attacks

Affected Endpoints:

```
http://localhost:5000
http://localhost:5000/robots.txt
http://localhost:5000/sitemap.xml
```

Recommended Fix:

Configure HTTP headers:

```
Content-Security-Policy: default-src 'self'
```

---

### Low Severity

**Server Leaks Version Information**

The application exposes server details via response headers.

Example:

```
Werkzeug/3.1.6 Python/3.12.3
```

Risk:

Attackers may use this information to identify vulnerabilities.

Recommended Fix:

Disable server header exposure.

---

# 8. Conclusion

This POC demonstrates how **OWASP ZAP can be used to perform Dynamic Application Security Testing on Python microservices**.

The scan successfully identified:

* Missing Content Security Policy header
* Server information disclosure

No high-severity vulnerabilities were detected.

Integrating DAST in the development pipeline helps detect runtime vulnerabilities early and strengthens overall application security.

---

# 9. Contact Information

| Name             | Email |
| ---------------- | ----- |
| Abhinav Sikarwar |[abhinav.sikarwar@mygurukulam.co](abhinav.sikarwar@mygurukulam.co)    |

---

# 10. References

| Reference                                                                                                      | Description             |
| -------------------------------------------------------------------------------------------------------------- | ----------------------- |
| [https://www.zaproxy.org/docs/](https://www.zaproxy.org/docs/)                                                 | OWASP ZAP Documentation |

---


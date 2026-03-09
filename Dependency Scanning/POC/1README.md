# Python Dependency Scanning – "TRIVY" 

---

## Author Information

| Author           | Created on | Version | Last edited on | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 08-03-2026 | v1.0    | 08-03-2026     | Aayush Verma|Shreya Jaiswal|Ashwani     |

---

## Table of Contents

 [1. Purpose](#1-purpose)
 [2. Scan Architecture](#2-scan-architecture)
 [3. Environment Setup](#3-environment-setup)
 [4. Trivy Scan Workflow](#4-trivy-scan-workflow)
 [5. Attendance API Scan](#5-attendance-api-scan)
 [6. Notification Worker Scan](#6-notification-worker-scan)
 [7. Vulnerability Summary](#7-vulnerability-summary)
 [8. Conclusion](#9-conclusion)

---

## 1. Purpose

Dependency scanning identifies vulnerabilities present in third-party libraries used by an application.

Most modern applications rely on external packages such as:

* Flask
* Jinja2
* Werkzeug

If these dependencies contain known vulnerabilities, attackers may exploit them to compromise the application.

In this POC, **Trivy** was used to scan the project dependencies for vulnerabilities.

---

## 2. Scan Architecture

<img width="420" height="338" alt="image" src="https://github.com/user-attachments/assets/93a15591-46ea-49ad-9a21-49525d6e628a" />

---

## 3. Environment Setup

### Install Trivy

```bash
sudo snap install trivy
```

Verify installation:

```bash
trivy --version
```

Example output:

```
Version: 0.52.2
```

<img width="952" height="152" alt="image" src="https://github.com/user-attachments/assets/ec665ff9-420c-44f7-8556-c70a6b072526" />


---

## 4. Trivy Scan Workflow

The dependency scan was performed using **Trivy filesystem scan**.

Steps performed:

1. Navigate to project directory
2. Run Trivy scan
3. Analyze vulnerability results
4. Export report file

---

## 5. Attendance API Scan

### Step 1 — Navigate to Project

```bash
cd ~/attendance
```

### Step 2 — Run Trivy Scan

```bash
trivy fs .
```

<img width="1483" height="532" alt="image" src="https://github.com/user-attachments/assets/81d1327c-24f5-4270-8af9-98460083f933" />

---

### Step 3 — Generate Scan Report

```bash
trivy fs --format table -o trivy_attendance_report.txt .
```

<img width="1278" height="892" alt="image" src="https://github.com/user-attachments/assets/86187476-2f9c-40b3-9afa-9b60e84db060" />
<img width="1283" height="151" alt="image" src="https://github.com/user-attachments/assets/02d37463-08d2-47cd-84ea-ae9eba27c2b0" />

---

### Scan Result

Target scanned:

```
attendance_api/poetry.lock
```

Summary:

| Severity | Count |
| -------- | ----- |
| Low      | 1     |
| Medium   | 11    |
| High     | 1     |
| Critical | 0     |
| Total    | 13    |

Detected vulnerable libraries:

| Library  | Vulnerability  |
| -------- | -------------- |
| Flask    | CVE-2026-27205 |
| Jinja2   | CVE-2024-22195 |
| Werkzeug | CVE-2024-34069 |

---

## 6. Notification Worker Scan

### Step 1 — Navigate to Project

```bash
cd ~/notification-worker
```

### Step 2 — Run Trivy Scan

```bash
trivy fs .
```
---

### Step 3 — Generate Report

```bash
trivy fs --format table -o trivy_notification_report.txt .
```

<img width="1600" height="406" alt="image" src="https://github.com/user-attachments/assets/63194a51-1839-4b3d-842a-00b21b3bd02f" />

<img width="1600" height="180" alt="image" src="https://github.com/user-attachments/assets/e11f1578-7667-4723-96f4-420902dca47f" />

---

### Scan Result

Target scanned:

```
requirements.txt
```

Result:

| Severity | Count |
| -------- | ----- |
| Low      | 0     |
| Medium   | 0     |
| High     | 0     |
| Critical | 0     |

Result:

```
Clean (no vulnerabilities detected)
```
---

## 7. Vulnerability Summary

| Service             | Vulnerabilities             |
| ------------------- | --------------------------- |
| Attendance API      | 13 vulnerabilities detected |
| Notification Worker | No vulnerabilities detected |

Most vulnerabilities originate from outdated Python packages.

---


## 8. Conclusion

Dependency vulnerability scanning was successfully performed using **Trivy**.

Key observations:

* Attendance API contains **multiple vulnerable dependencies**.
* Notification Worker dependencies are **secure**.
* Updating vulnerable packages will reduce the attack surface.

Regular dependency scanning should be integrated into the **CI/CD pipeline** to maintain application security.

---

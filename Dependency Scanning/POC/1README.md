# Dependency Vulnerability Scanning using Trivy

---

# Table of Contents

* [1. Purpose](#1-purpose)
* [5. Scan Architecture](#5-scan-architecture)
* [6. Environment Setup](#6-environment-setup)
* [7. Trivy Scan Workflow](#7-trivy-scan-workflow)
* [8. Attendance API Scan](#8-attendance-api-scan)
* [9. Notification Worker Scan](#9-notification-worker-scan)
* [10. Vulnerability Summary](#10-vulnerability-summary)
* [11. Remediation](#11-remediation)
* [12. Conclusion](#12-conclusion)

---

# 1. Purpose

Dependency scanning identifies vulnerabilities present in third-party libraries used by an application.

Most modern applications rely on external packages such as:

* Flask
* Jinja2
* Werkzeug

If these dependencies contain known vulnerabilities, attackers may exploit them to compromise the application.

In this POC, **Trivy** was used to scan the project dependencies for vulnerabilities.

---

# 5. Scan Architecture

```text
Application Source Code
        │
        ▼
Dependency Files
(poetry.lock / requirements.txt)
        │
        ▼
Trivy Filesystem Scan
        │
        ▼
Vulnerability Database Lookup
        │
        ▼
Detected CVEs
        │
        ▼
Security Report Generated
```

---

# 6. Environment Setup

### Install Trivy

Verify installation:

```bash
trivy --version
```

Example output:

```
Version: 0.52.2
```

📸 **Screenshot Placeholder**

```
Add Screenshot: Trivy installation verification
```

---

# 7. Trivy Scan Workflow

The dependency scan was performed using **Trivy filesystem scan**.

Steps performed:

1. Navigate to project directory
2. Run Trivy scan
3. Analyze vulnerability results
4. Export report file

---

# 8. Attendance API Scan

### Step 1 — Navigate to Project

```bash
cd ~/attendance
```

📸 **Screenshot**

```
Add Screenshot: Attendance API project directory
```

---

### Step 2 — Run Trivy Scan

```bash
trivy fs .
```

📸 **Screenshot**

```
Add Screenshot: Trivy scanning attendance API
```

---

### Step 3 — Generate Scan Report

```bash
trivy fs --format table -o trivy_attendance_report.txt .
```

📸 **Screenshot**

```
Add Screenshot: Trivy report generation
```

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

📸 **Screenshot**

```
Add Screenshot: Trivy vulnerability results for Attendance API
```

---

# 9. Notification Worker Scan

### Step 1 — Navigate to Project

```bash
cd ~/notification-worker
```

📸 **Screenshot**

```
Add Screenshot: Notification worker directory
```

---

### Step 2 — Run Trivy Scan

```bash
trivy fs .
```

📸 **Screenshot**

```
Add Screenshot: Trivy scanning notification worker
```

---

### Step 3 — Generate Report

```bash
trivy fs --format table -o trivy_notification_report.txt .
```

📸 **Screenshot**

```
Add Screenshot: Trivy notification report
```

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

📸 **Screenshot**

```
Add Screenshot: Notification worker clean scan
```

---

# 10. Vulnerability Summary

| Service             | Vulnerabilities             |
| ------------------- | --------------------------- |
| Attendance API      | 13 vulnerabilities detected |
| Notification Worker | No vulnerabilities detected |

Most vulnerabilities originate from outdated Python packages.

---

# 11. Remediation

To fix vulnerabilities, dependencies should be upgraded.

Example:

```bash
pip install --upgrade flask jinja2 werkzeug
```

Or update dependency definitions in:

* `poetry.lock`
* `requirements.txt`

---

# 12. Conclusion

Dependency vulnerability scanning was successfully performed using **Trivy**.

Key observations:

* Attendance API contains **multiple vulnerable dependencies**.
* Notification Worker dependencies are **secure**.
* Updating vulnerable packages will reduce the attack surface.

Regular dependency scanning should be integrated into the **CI/CD pipeline** to maintain application security.

---

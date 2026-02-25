# Proof of Concept (POC): DAST using OWASP ZAP on Python Attendance & Notification Application

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

OWASP ZAP GUI opens successfully.

This tool will perform dynamic security scanning.

---

# 6. Step 4: Create Python Attendance and Notification Application

Create application file:

```bash
mkdir dast-test
cd dast-test
nano attendance_app.py
```

Paste the following code:

```python
from flask import Flask, request

app = Flask(__name__)

@app.route("/")
def home():
    return "Attendance Service Running"

@app.route("/login")
def login():
    username = request.args.get("username")
    return "Welcome " + username

@app.route("/notify")
def notify():
    msg = request.args.get("msg")
    return "Notification sent: " + msg

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

Save file.

This application contains intentionally vulnerable endpoints.

---

# 7. Step 5: Install Flask

Install Flask:

```bash
pip install flask
```

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

OWASP ZAP performs the following actions:

* Spider Scan → discovers endpoints
* Passive Scan → analyzes responses
* Active Scan → sends attack payloads

Discovered endpoints:

```
/
/login
/notify
```

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

Report is successfully generated.

---

# 12. Step 10: View Security Report

Copy report to Downloads folder:

```bash
cp "2026-02-25-ZAP-Report-.html" /mnt/c/Users/lenovo/Downloads/
```

Open Downloads folder in Windows.

Double-click:

```
2026-02-25-ZAP-Report-.html
```

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

# 17. Files Generated in this POC

```
attendance_app.py
2026-02-25-ZAP-Report-.html
ZAP_2.16.1/
```

---

# Python CI Security Checks – Dependency Scanning Doc

---

## Author Information

| Author           | Created on | Version | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 21-02-2026 | v1.0    | 21-02-2026     | Aayush Verma|Shreya Jaiswal|Ashwani     |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Dependency Scanning](#2-what-is-dependency-scanning)
3. [Why Dependency Scanning is Required](#3-why-dependency-scanning-is-required)
4. [Dependency Scanning Workflow Diagram](#4-dependency-scanning-workflow-diagram)
5. [Dependency Scanning Tools](#5-dependency-scanning-tools)
6. [Tools Comparison](#6-tools-comparison)
7. [Advantages of Dependency Scanning](#7-advantages-of-dependency-scanning)
8. [Proof of Concept (POC)](#8-proof-of-concept-poc)
9. [Best Practices](#9-best-practices)
10. [Recommendation and Conclusion](#10-recommendation-and-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

# 1. Introduction

This document provides a comprehensive overview of Dependency Scanning implemented as part of Continuous Integration (CI) security checks for Python-based attendance and notification services. It explains the purpose, workflow, tools, comparison, advantages, best practices, and recommendations for integrating dependency scanning into the CI pipeline.

Attendance and notification services rely on multiple third-party Python libraries and packages. These dependencies may contain known security vulnerabilities that can expose the system to risks such as data breaches, unauthorized access, or system compromise.

Dependency scanning helps identify vulnerabilities in third-party libraries before deployment, ensuring secure and reliable application operation. Integrating dependency scanning into the CI pipeline improves security posture and ensures safe use of external dependencies.

---

# 2. What is Dependency Scanning

Dependency scanning is a security testing process that analyzes third-party libraries and dependencies used in an application to identify known vulnerabilities.

It scans dependency files such as:

* requirements.txt
* Pipfile
* poetry.lock

### Key Characteristics

| Feature                 | Description                         |
| ----------------------- | ----------------------------------- |
| Dependency Analysis     | Scans third-party libraries         |
| Vulnerability Detection | Identifies known vulnerabilities    |
| Automated Scanning      | Can be integrated into CI/CD        |
| Security Improvement    | Prevents use of vulnerable packages |

Dependency scanning ensures Python dependencies used in attendance and notification services are secure.

---

# 3. Why Dependency Scanning is Required

| Purpose                        | Description                                    | Outcome                       |
| ------------------------------ | ---------------------------------------------- | ----------------------------- |
| Detect Vulnerable Dependencies | Identifies insecure Python libraries           | Improves application security |
| Prevent Security Risks         | Prevents use of vulnerable packages            | Ensures secure deployment     |
| Improve CI/CD Security         | Enables automated dependency checks            | Improves pipeline security    |
| Compliance and Governance      | Meets security standards                       | Ensures compliance            |
| Protect Application Data       | Prevents exploitation via vulnerable libraries | Improves system security      |

Dependency scanning ensures safe and secure use of third-party libraries.

---

# 4. Dependency Scanning Workflow Diagram

<img width="708" height="467" alt="image" src="https://github.com/user-attachments/assets/b2a0d315-61bd-416a-8d49-2af5e6629ca2" />

This workflow ensures secure dependency management.

---

# 5. Dependency Scanning Tools

| Tool                   | Description                             | Advantages                       | Limitations               |
| ---------------------- | --------------------------------------- | -------------------------------- | ------------------------- |
| Safety                 | Python dependency vulnerability scanner | Easy to use, Python-specific     | Limited advanced features |
| Snyk                   | Enterprise dependency scanning tool     | Advanced vulnerability detection | Paid tool                 |
| Trivy                  | Open-source vulnerability scanner       | Fast and reliable                | Requires configuration    |
| OWASP Dependency-Check | Open-source dependency scanner          | Comprehensive scanning           | Slower scanning process   |

These tools help detect vulnerabilities in Python dependencies.

---

# 6. Tools Comparison

| Tool                   | Open Source | Python Support | CI/CD Integration | Enterprise Ready |
| ---------------------- | ----------- | -------------- | ----------------- | ---------------- |
| Safety                 | Yes         | Yes            | Yes               | Limited          |
| Snyk                   | No          | Yes            | Yes               | Yes              |
| Trivy                  | Yes         | Yes            | Yes               | Yes              |
| OWASP Dependency-Check | Yes         | Yes            | Yes               | Yes              |

---

# 7. Advantages of Dependency Scanning

| Advantage                       | Description                |
| ------------------------------- | -------------------------- |
| Detects vulnerable dependencies | Prevents security risks    |
| Improves application security   | Protects system integrity  |
| CI/CD integration               | Enables automated scanning |
| Prevents vulnerable deployments | Ensures secure application |
| Compliance support              | Meets security standards   |

Dependency scanning improves application security and reliability.

---

# 8. Proof of Concept (POC)

This section will include demonstration of dependency scanning implementation for attendance and notification Python services.

POC will include:

* Dependency scanning tool execution
* Vulnerability report generation
* CI pipeline integration

*(To be added as per implementation)*

---

# 9. Best Practices

| Practice                         | Reason                                 |
| -------------------------------- | -------------------------------------- |
| Scan dependencies in CI pipeline | Ensures continuous security validation |
| Regularly update dependencies    | Prevents use of vulnerable libraries   |
| Use reliable scanning tools      | Ensures accurate detection             |
| Monitor vulnerability reports    | Improves security                      |
| Fix vulnerabilities immediately  | Prevents exploitation                  |

Following best practices ensures secure dependency management.

---

# 10. Recommendation and Conclusion

## Recommended Tool: Trivy

Trivy is recommended for dependency scanning of attendance and notification Python services.

### Reasons for Choosing Trivy

| Reason             | Explanation                                |
| ------------------ | ------------------------------------------ |
| Open Source        | No licensing cost                          |
| Fast and Reliable  | Efficient vulnerability detection          |
| CI/CD Integration  | Easy integration with pipelines            |
| Enterprise Ready   | Widely used in enterprise environments     |
| Multi-purpose Tool | Supports dependency and container scanning |

### Why Other Tools Not Selected

| Tool                   | Limitation                    |
| ---------------------- | ----------------------------- |
| Safety                 | Limited enterprise features   |
| Snyk                   | Paid tool, licensing required |
| OWASP Dependency-Check | Slower scanning process       |

---

## Final Conclusion

Dependency scanning is essential for ensuring secure use of third-party Python libraries in attendance and notification services. It helps identify vulnerabilities in dependencies and prevents insecure deployments.

Trivy is the recommended tool due to its open-source availability, fast scanning, enterprise readiness, and seamless CI/CD integration. Implementing Trivy in the CI pipeline ensures secure, reliable, and compliant dependency management.

---

# 11. Contact Information

| Name             | Email                                                                     |
| ---------------- | ------------------------------------------------------------------------- |
| Abhinav Sikarwar | [abhinav.sikarwar@mygurukulam.co](mailto:abhinav.sikarwar@mygurukulam.co) |

---

# 12. References

| Reference             | Description                               |
| --------------------- | ----------------------------------------- |
| Trivy Documentation   | [Official Trivy documentation](http://trivy.dev/docs/latest/guide/)              |
---

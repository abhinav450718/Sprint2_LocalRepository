# Authorization (Authz) Setup

---

## Author Information

| Author           | Created on | Version | Last edited on | L0 Reviewer  | L1 Reviewer    | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ------------ | -------------- | ----------- |
| Abhinav Sikarwar | 07-03-2026 | v1.0    | 07-03-2026     | Aayush Verma | Shreya Jaiswal | Ashwani     |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Objective of the POC](#2-objective-of-the-poc)
3. [Prerequisites](#3-prerequisites)
4. [Repository Setup](#4-repository-setup)
5. [Adding Users and Assigning Roles](#5-adding-users-and-assigning-roles)
6. [Configuring Branch Protection Rules](#6-configuring-branch-protection-rules)
7. [Pull Request Authorization Workflow](#7-pull-request-authorization-workflow)
8. [Authorization Scenario Demonstration](#8-authorization-scenario-demonstration)
9. [Audit Trail Verification](#9-audit-trail-verification)
10. [POC Validation](#10-poc-validation)
11. [Conclusion](#11-conclusion)
12. [References](#12-references)

---

# 1. Introduction

Authentication verifies the identity of a user accessing a system, while Authorization determines the actions the authenticated user is allowed to perform.

In GitHub repositories, authorization is implemented through role-based access permissions and branch protection rules. These mechanisms ensure that only authorized users can perform actions such as pushing code, merging pull requests, or modifying repository settings.

This document demonstrates a Proof of Concept (POC) for implementing authorization controls in a GitHub repository.

---

# 2. Objective of the POC

The objective of this POC is to demonstrate how authorization can be implemented in a GitHub repository to control access and maintain secure development workflows.

Key goals include:

* Implement role-based access control for repository users.
* Protect critical branches using branch protection rules.
* Enforce pull request based code integration.
* Track repository activities through audit logs.

---

# 3. Prerequisites

Before starting the setup, ensure the following requirements are met:

* A GitHub account.
* A GitHub repository created for testing.
* Repository owner or admin access.
* At least two additional GitHub users to demonstrate role-based access.

---

# 4. Repository Setup

Step 1
Log in to GitHub and navigate to your repository.

Step 2
Open the repository dashboard.

Step 3
Ensure the repository has a default branch such as **main**.

```
Repository Name: Authz-Setup
Default Branch: main
```
<img width="1461" height="500" alt="image" src="https://github.com/user-attachments/assets/6af2dfae-1820-4119-9b81-7eb95cf82eff" />

---

# 5. Adding Users and Assigning Roles

GitHub allows repository owners to assign different access levels to users.

Available roles include:

| Role     | Description                            |
| -------- | -------------------------------------- |
| Read     | View repository contents only          |
| Write    | Push commits and create pull requests  |
| Maintain | Manage pull requests and merge changes |
| Admin    | Full control of repository settings    |

### Steps

Step 1
Navigate to:

```
Repository → Settings
```

Step 2
Select:

```
Collaborators and Teams
```

Step 3
Click **Add people**.

Step 4
Add users and assign roles.

Example configuration:

| User        | Role     |
| ----------- | -------- |
| Developer A | Write    |
| Developer B | Write    |
| Maintainer  | Maintain |

<img width="1899" height="861" alt="image" src="https://github.com/user-attachments/assets/211b3ddb-7f0f-4427-9b64-2620b51a8255" />


---

# 6. Configuring Branch Protection Rules

Branch protection prevents unauthorized changes to critical branches such as **main**.

### Steps

Step 1
Navigate to:

```
Repository → Settings → Branches
```

Step 2
Click **Add Branch Protection Rule**.

Step 3
Configure the following settings:

Branch name pattern:

```
main
```

Enable:

* Require pull request before merging
* Require approvals before merging
* Prevent force pushes
* Prevent branch deletion

<img width="1084" height="257" alt="image" src="https://github.com/user-attachments/assets/e466e8a7-3ae9-4c39-a6a9-b1175be46e35" />
<img width="1040" height="467" alt="image" src="https://github.com/user-attachments/assets/cf45a848-e6c2-4201-b9c4-b5fca8adbe1e" />


---

# 7. Pull Request Authorization Workflow

The implemented workflow ensures controlled code integration.

### Workflow Steps

1. Developer creates a new branch.
2. Developer commits changes to the branch.
3. Developer creates a pull request.
4. Maintainer reviews the pull request.
5. Maintainer approves and merges the changes.

### Example Workflow

```
Developer → Create Branch → Commit Code → Open Pull Request
Maintainer → Review Pull Request → Approve → Merge
```

---

# 8. Authorization Scenario Demonstration

This scenario demonstrates how role-based authorization works in a real development workflow.

### Participants

| User        | Role     | Responsibility                          |
| ----------- | -------- | --------------------------------------- |
| Developer A | Write    | Creates branch, commits code, raises PR |
| Developer B | Write    | Reviews and approves PR                 |
| Maintainer  | Maintain | Merges PR                               |

---

### Step 1: Developer A Creates Branch and Commits Code

Developer A creates a branch and commits a new file.

Example:

```
Branch: hardbro-786-patch-1
File Added: README.md
```
<img width="1285" height="574" alt="image" src="https://github.com/user-attachments/assets/b131c77e-2a9f-4c59-a190-a4c5d4f8d1eb" />


---

### Step 2: Developer A Creates Pull Request

Developer creates a branch and made a pull request 
---

### Step 3: Pull Request Requires Approval

Because branch protection rules require approval:

* Developer A cannot approve their own PR.
* PR remains in **pending review** state.

<img width="1809" height="925" alt="image" src="https://github.com/user-attachments/assets/0daf543c-b1cd-472d-83cf-5be87e9f6dea" />


---

### Step 4: Developer B Approves the Pull Request

Developer B reviews the PR and approves it.

```
Review → Approve
```

<img width="1336" height="709" alt="image" src="https://github.com/user-attachments/assets/a61bcd11-5073-4397-8eae-026b3cf11849" />


---

### Step 5: Maintainer Merges Pull Request

Maintainer performs the merge after approval.

```
Merge Pull Request
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f6be8fe4-ddf7-4089-8e31-c469bdf59a49" />


---

### Step 6: Branch Deletion Restriction

Users with **Write access cannot delete protected branches**.

Attempting to delete **main** results in:

```
Branch deletion blocked by protection rules
```
<img width="1772" height="1004" alt="image" src="https://github.com/user-attachments/assets/f718e3bc-b111-4e53-85df-60e5ae591f59" />

---

# 9. Audit Trail Verification

GitHub maintains logs of repository activities for transparency and accountability.

Examples of tracked activities:

| Activity           | Description                                       |
| ------------------ | ------------------------------------------------- |
| Commits            | Records code changes and author information       |
| Pull Requests      | Tracks creation, review, and merging              |
| Repository Changes | Logs permission updates and configuration changes |

### Steps to View Logs

Navigate to:

```
Repository → Insights → Contributors
```

or

```
Repository → Pull Requests → Activity
```
<img width="1615" height="749" alt="image" src="https://github.com/user-attachments/assets/67ceb6d2-bf5f-44db-8f08-fb9321a96a9e" />
<img width="1896" height="964" alt="image" src="https://github.com/user-attachments/assets/2dad8253-3a45-425a-afd0-a98cdfdd27d6" />
<img width="1919" height="512" alt="image" src="https://github.com/user-attachments/assets/650f5c3d-8d58-4829-995f-c23c2b159161" />


---

# 10. POC Validation

To validate the authorization setup:

| Test Scenario                            | Expected Result                   |
| ---------------------------------------- | --------------------------------- |
| Developer tries to push directly to main | Push should be blocked            |
| Developer creates pull request           | PR should be created successfully |
| Developer with Write access reviews PR   | Approval allowed                  |
| Maintainer merges PR                     | Merge successful                  |
| Developer attempts to delete main branch | Operation blocked                 |

This confirms that branch protection and role-based access control are functioning correctly.

---

# 11. Conclusion

This POC demonstrates how authorization can be implemented in a GitHub repository using role-based access control and branch protection policies.

The implemented setup ensures secure repository access, controlled code integration, and clear audit trails for all activities.

Such authorization mechanisms help maintain code security, accountability, and structured collaboration within development teams.

---

# 12. References

| Link                                                                                                         | Description                   |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------- |
| [https://faisalakhan98.atlassian.net/browse/SCRUM-115](https://faisalakhan98.atlassian.net/browse/SCRUM-115) | Reference Authz documentation |

---

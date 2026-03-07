# Authorization (Authz) Setup POC in GitHub Repository
---

| Author           | Created on | Version |  Last edited on | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- |  -------------- | ----------- | ----------- | ----------- |
| Abhinav Sikarwar | 07-03-2026 | v1.0    |  07-03-2026     |Aayush Verma |Shreya Jaiswal|Ashwani     |

---

# Table of Contents

1. Introduction
2. Objective of the POC
3. Prerequisites
4. Repository Setup
5. Adding Users and Assigning Roles
6. Configuring Branch Protection Rules
7. Pull Request Authorization Workflow
8. Audit Trail Verification
9. POC Validation
10. Conclusion
11. References

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

Example:

```
Repository Name: authz-poc-demo
Default Branch: main
```

### Screenshot

(Add screenshot of repository dashboard here)

```
![Repository Dashboard](screenshots/repo-dashboard.png)
```

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

| User       | Role     |
| ---------- | -------- |
| Developer  | Write    |
| Maintainer | Maintain |
| Repo Owner | Admin    |

### Screenshot

(Add screenshot of collaborators configuration)

```
![Collaborators Setup](screenshots/collaborators.png)
```

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

### Screenshot

(Add screenshot of branch protection rule)

```
![Branch Protection Rule](screenshots/branch-protection.png)
```

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

### Screenshot

(Add screenshot of pull request creation)

```
![Pull Request](screenshots/pull-request.png)
```

---

# 8. Audit Trail Verification

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

### Screenshot

(Add screenshot showing commit history or PR activity)

```
![Audit Trail](screenshots/audit-trail.png)
```

---

# 9. POC Validation

To validate the authorization setup:

| Test Scenario                            | Expected Result                   |
| ---------------------------------------- | --------------------------------- |
| Developer tries to push directly to main | Push should be blocked            |
| Developer creates pull request           | PR should be created successfully |
| Maintainer reviews PR                    | PR approval option available      |
| Maintainer merges PR                     | Merge successful                  |

This confirms that branch protection and role-based access control are functioning correctly.

---

# 10. Conclusion

This POC demonstrates how authorization can be implemented in a GitHub repository using role-based access control and branch protection policies.

The implemented setup ensures secure repository access, controlled code integration, and clear audit trails for all activities.

Such authorization mechanisms help maintain code security, accountability, and structured collaboration within development teams.

---

# 11. References

| Link                                                                                                                         | Description                            |
| ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| [https://docs.github.com/en/authentication](https://docs.github.com/en/authentication)                                       | GitHub authentication documentation    |
| [https://docs.github.com/en/repositories/configuring-branches](https://docs.github.com/en/repositories/configuring-branches) | GitHub branch protection documentation |
| [https://docs.github.com/en/organizations/managing-access](https://docs.github.com/en/organizations/managing-access)         | GitHub access management               |

---

# Lab 5 – IAM Privilege Risk, Detection & Least-Privilege Remediation

## Overview

This lab focuses on **identity and access management (IAM) risk analysis**, **audit-based detection**, and **least-privilege remediation** in AWS. It demonstrates how overly permissive IAM policies can introduce **privilege escalation risk**, how such activity can be detected using **AWS CloudTrail**, and how to remediate the issue by enforcing least-privilege access.

This lab serves as a **capstone** to the cloud security series, tying together identity security, logging, investigation, and response. All activities were performed using **free AWS services**, ensuring no operational cost.

---

## Objectives

* Identify high-risk IAM permissions that can lead to privilege escalation
* Understand why specific IAM actions are considered dangerous
* Detect IAM changes using AWS CloudTrail Event History
* Apply least-privilege principles to remediate IAM risk
* Validate remediation by removing excessive permissions

---

## AWS Services Used

* **AWS Identity and Access Management (IAM)** – Policy creation and identity management
* **AWS CloudTrail (Event History)** – Audit logging and investigation

> Note: No CloudTrail trails, GuardDuty, Security Hub, AWS Config, or other paid services were enabled.

---

## Scenario Description

A review of IAM permissions identified a policy that granted **excessive privileges** related to identity management. Permissions allowing user creation, policy attachment, and access key generation were evaluated due to their potential to enable **privilege escalation** and long-lived credential abuse.

The objective of this lab was to analyse this risk, observe how such actions are logged, and then remediate the issue by enforcing least privilege.

---

## Lab Steps

### 1. Identify High-Risk IAM Permissions

A custom IAM policy was created to demonstrate common high-risk permissions:

* `iam:CreateUser`
* `iam:AttachUserPolicy`
* `iam:CreateAccessKey`
* `Resource: "*"`

These permissions are considered dangerous because they allow the creation of new identities, the attachment of powerful policies (including administrative access), and the generation of long-lived credentials.

---

### 2. Controlled Policy Attachment

The policy was attached to a **temporary test IAM user** to generate a realistic audit trail. The user was created without console access and was used solely for controlled testing.

This step ensured that IAM activity could be observed without impacting production resources.

---

### 3. Detection Using CloudTrail

AWS CloudTrail Event History was used to detect and review IAM activity:

* Time range was adjusted to capture recent events
* Events were filtered using:

  * **Event source:** `iam.amazonaws.com`

This revealed sensitive IAM actions including user creation, policy attachment, and access key generation.

---

### 4. Investigation and Analysis

Individual IAM events were analysed to determine:

* **eventName** – Specific IAM action performed
* **eventSource** – AWS service handling the request
* **userIdentity** – Identity responsible for the action
* **sourceIPAddress** – Origin of the request
* **userAgent** – Method used (console or CLI)

This analysis demonstrates how IAM misuse would be investigated during a real security incident.

---

### 5. Remediation and Least Privilege Enforcement

After confirming the risk, remediation steps were applied:

* The risky IAM policy was detached and deleted
* The temporary test IAM user was removed
* Excessive permissions were eliminated entirely

This enforced the **principle of least privilege** and removed the potential escalation path.

---

### 6. Validation

After remediation, attempts to perform the same privileged actions would result in **AccessDenied**, confirming that the excessive permissions had been successfully removed.

---

## Key Security Concepts Demonstrated

* IAM privilege escalation risk awareness
* Least-privilege policy design
* Detection of identity-related security events
* Audit-driven incident investigation
* Identity-focused defense-in-depth

---

## Learning Outcomes

By completing this lab, the following skills were developed:

* Ability to identify and reason about dangerous IAM permissions
* Practical experience detecting IAM changes using CloudTrail
* Understanding of how IAM misuse is investigated in real environments
* Confidence applying least-privilege remediation

---

## Conclusion

This lab demonstrated how excessive IAM permissions can introduce serious security risks and how AWS-native logging can be used to detect and investigate such activity. By enforcing least privilege and validating remediation, the lab completed the full security lifecycle of **risk identification, detection, investigation, and response**.

This lab strongly aligns with **AWS Security – Specialty** exam objectives and reflects real-world cloud security engineering practices.

---

## Cleanup

* Temporary IAM user deleted
* Risky IAM policy deleted
* No resources or paid services left enabled

---

## Screenshots

Screenshots captured for this lab include:

* CloudTrail Event History
![Event Timeline](screenshots/cloudtrail-event.png)

* JSON File Showing Policies Included
![JSON File](screenshots/JSON.png)

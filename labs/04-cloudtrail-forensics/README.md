# Lab 4 – CloudTrail Forensics: Investigating High-Risk IAM Activity

## Overview

This lab focuses on **cloud forensics and incident investigation** using **AWS CloudTrail Event History**. Unlike previous labs that emphasised secure design, detection, and compliance, this lab demonstrates how to **investigate sensitive security events after they occur**, using audit logs as forensic evidence.

The lab simulates a realistic scenario in which **high-risk IAM management actions** (such as user creation and privilege-related changes) are reviewed to determine **who performed the action, from where, and using what method**.

No paid AWS services were enabled during this lab, ensuring **zero operational cost**.

---

## Objectives

* Use AWS CloudTrail Event History for forensic investigation
* Identify high-risk IAM management actions
* Attribute actions to a specific identity, source IP, and user agent
* Analyse CloudTrail event fields relevant to incident response
* Understand the role of audit logs in cloud security investigations

---

## AWS Services Used

* **AWS CloudTrail (Event History)** – Management event logging and investigation
* **AWS IAM** – Identity and access management actions

> Note: No CloudTrail trails, CloudWatch Logs, Athena queries, or AWS Config resources were created.

---

## Scenario Description

During routine security monitoring, a sensitive IAM action was detected involving the creation of a new IAM user. As IAM changes can significantly impact account security, this activity was treated as **potentially high-risk** and investigated using CloudTrail.

The goal was to reconstruct the event timeline and analyse the context of the action to determine its legitimacy and security impact.

---

## Lab Steps

### 1. Access CloudTrail Event History

* Navigated to **AWS CloudTrail → Event history**
* Adjusted the time range to ensure recent events were visible
* Ensured the correct AWS region was selected

---

### 2. Filter for IAM Activity

* Applied a filter using:

  * **Event source:** `iam.amazonaws.com`
* This narrowed results to IAM-related management actions such as:

  * `CreateUser`
  * `AttachUserPolicy`
  * `CreateAccessKey`

This step established a focused investigation scope.

---

### 3. Identify a High-Risk IAM Event

* Located a **CreateUser** event within the filtered results
* Selected the event for detailed analysis

IAM user creation is considered a **high-risk action** because it introduces a new identity that could be abused if misconfigured.

---

### 4. Forensic Analysis of the Event

The following CloudTrail fields were analysed:

* **eventName** – The specific API action performed (`CreateUser`)
* **eventSource** – The AWS service that processed the request (`iam.amazonaws.com`)
* **userIdentity** – The identity that performed the action
* **sourceIPAddress** – The origin of the request
* **userAgent** – The tool used (AWS Console, browser, or CLI)
* **requestParameters** – Details of the resource affected (username created)

This information provided full attribution of the action and supported timeline reconstruction.

---

### 5. Timeline Review

* Returned to the Event History view
* Reviewed surrounding IAM events to understand the broader activity context
* Considered whether related actions (e.g., policy attachment or key creation) occurred

This step mirrors real-world incident response, where analysts assess whether an action is isolated or part of a broader sequence.

---

## Key Security Concepts Demonstrated

* Cloud forensic investigation using audit logs
* Identification of high-risk IAM actions
* Attribution of cloud activity to identities and IP addresses
* Incident timeline reconstruction
* Importance of logging and monitoring in cloud environments

---

## Learning Outcomes

By completing this lab, the following skills were developed:

* Practical investigation of AWS CloudTrail events
* Understanding of which IAM actions are security-sensitive
* Ability to interpret CloudTrail event metadata
* Incident response reasoning in cloud-native environments

---

## Conclusion

This lab demonstrated how AWS CloudTrail supports **forensic investigation and incident response** by providing detailed audit logs of management activity. By analysing a high-risk IAM action, it was possible to attribute the event to a specific identity, source, and method, illustrating how cloud security investigations are conducted in practice.

This lab builds on earlier work in detection and compliance by adding **post-event analysis**, completing a critical component of a defense-in-depth cloud security strategy.

---

## Cleanup

* The test IAM user created during the lab was deleted after analysis
* No additional AWS services were left enabled
* No ongoing costs were incurred

---

## Screenshots

Screenshots captured for this lab include:

* CloudTrail Event History filtered for IAM activity
![IAM Event Timeline](screenshots/iam-event-timeline.png)

* Detailed CloudTrail event view for a high-risk IAM actio
![Create User Details](screenshots/createuser-details.png)



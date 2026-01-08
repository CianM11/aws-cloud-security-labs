AWS Cloud Security Lab – IAM, Secure Storage & Audit Logging
Overview

This lab focused on building and securing a basic AWS cloud environment while applying core cloud security principles. The objective was to understand how identity, access control, and audit logging work together in a real-world cloud setting, and how common misconfigurations can be detected and remediated.

The lab was designed and executed using AWS Free Tier services.

Objectives

Deploy a basic AWS environment using best-practice defaults

Apply least-privilege access using IAM roles instead of static credentials

Secure cloud storage access

Enable and analyse CloudTrail logs for audit visibility

Simulate and remediate an IAM misconfiguration

Architecture

The lab environment consisted of:

A custom VPC with a single subnet

An EC2 instance running Amazon Linux

An IAM role attached to the instance

An S3 bucket used to test controlled access

AWS CloudTrail enabled for management event logging

The EC2 instance accessed AWS services using an IAM role, avoiding the use of access keys entirely.

Key Implementation Steps
1. Identity & Access Management

Created an IAM role for EC2 with scoped permissions

Attached the role directly to the instance

Verified access to S3 using role-based credentials

Confirmed no access keys were stored on the instance

This reinforced the importance of avoiding long-lived credentials and relying on AWS-managed identity.

2. Secure Storage Access

Created an S3 bucket with restricted access

Granted the EC2 IAM role permission to list and read objects

Validated that access was denied when permissions were removed

This demonstrated how IAM policies directly control access to cloud resources.

3. Audit Logging with CloudTrail

Enabled AWS CloudTrail for the account

Observed management events such as:

EC2 instance actions

IAM role usage

S3 access attempts

Analysed event details including:

Event source

Identity context

Timestamp and request metadata

CloudTrail provided full visibility into who did what, and when.

4. Misconfiguration Simulation & Remediation

Intentionally applied an overly permissive IAM policy

Verified that excessive permissions were granted

Detected the change using CloudTrail logs

Remediated the issue by tightening permissions to least privilege

This step highlighted how easy it is to introduce risk through IAM misconfiguration, and how logging is critical for detection.

Security Concepts Demonstrated

Least-privilege access

Role-based authentication

Secure cloud storage permissions

Auditability and accountability

Misconfiguration detection and response

Key Takeaways

IAM roles are significantly more secure than access keys

CloudTrail is essential for visibility and investigation

Misconfigurations are a common source of cloud risk

Secure defaults and monitoring reduce attack surface

Cleanup

All resources were terminated after completion to avoid ongoing costs.

Tools & Services Used

AWS EC2

AWS IAM

AWS S3

AWS CloudTrail

Amazon Linux

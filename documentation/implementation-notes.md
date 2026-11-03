# Implementation Notes

This document explains the components in the supplied architecture diagram and provides a checklist for recording the actual implementation.

## 1. Network
- VPC CIDR: `10.0.0.0/16`
- Public subnet A: `10.0.1.0/24`
- Public subnet B: `10.0.2.0/24`
- Private application subnet A: `10.0.11.0/24`
- Private application subnet B: `10.0.12.0/24`
- Private database subnet A: `10.0.21.0/24`
- Private database subnet B: `10.0.22.0/24`

Record the Internet Gateway, route-table associations, NAT Gateway placement, and network ACL/security-group rules from the deployed account.

## 2. Application tier
The diagram shows an Application Load Balancer distributing traffic to EC2 instances in two Availability Zones. The instances are managed by an Auto Scaling group using target tracking.

Record:
- Launch template name and AMI
- Instance type
- Auto Scaling minimum, desired, and maximum capacity
- Target-tracking metric and target value
- ALB listener protocol/port
- Target-group protocol/port and health-check path

## 3. Database tier
The diagram shows RDS Primary and Standby resources in separate Availability Zones. Record the actual RDS engine, instance class, storage, encryption, backup retention, and Multi-AZ status. Do not include credentials or connection strings.

## 4. Edge, security, and operations
The diagram includes Route 53, CloudFront, AWS WAF, Systems Manager Session Manager, CloudWatch, and SNS.

Record:
- Route 53 record type and target
- CloudFront origin and cache behaviors
- WAF Web ACL association and enabled rules
- Systems Manager registration and access method
- CloudWatch metrics, log groups, and alarms
- SNS topic and notification subscription type

## 5. Validation evidence
Add dated screenshots or concise test results for components actually deployed:
1. Application reachability through the intended public entry point.
2. Healthy ALB targets in both Availability Zones.
3. Auto Scaling response to the configured metric.
4. Application connectivity to the database.
5. RDS Multi-AZ status and failover understanding.
6. WAF behavior against a safe test rule, if configured.
7. CloudWatch alarm delivery to the SNS subscriber.

## 6. Security and publication
Before publishing, inspect every file. Remove credentials, access keys, private keys, passwords, tokens, `.env` files, database dumps, and personal information. Never upload AWS secret access keys or private SSH keys.

# Scalable and Highly Available Web Application on AWS

## Project overview
This project documents a scalable web application architecture on Amazon Web Services (AWS). The application tier is designed across two Availability Zones, using an Application Load Balancer and an EC2 Auto Scaling group. The database tier shows an Amazon RDS primary instance and standby instance in separate Availability Zones.

> **Implementation accuracy:** This repository documents the supplied architecture design. Do not describe resources as deployed or tested until you verify them in your AWS account. Replace deployment placeholders with actual values.

## Architecture
![AWS solution architecture](architecture/architecture-diagram.png)

Editable diagram source: [architecture/aws-scalable-web-app.drawio](architecture/aws-scalable-web-app.drawio)

## Request flow
1. Users access the application through its DNS name.
2. Route 53 resolves the domain.
3. CloudFront provides content delivery.
4. AWS WAF filters requests through a Web ACL associated with CloudFront.
5. Requests are forwarded to the Application Load Balancer.
6. The ALB distributes traffic to EC2 instances in private application subnets across two Availability Zones.
7. EC2 application instances access the RDS database tier.
8. EC2 Auto Scaling adjusts application capacity using a target-tracking policy.

## Network design
VPC CIDR: `10.0.0.0/16`

| Subnet | CIDR | Purpose |
|---|---|---|
| Public A | `10.0.1.0/24` | Public resources, including NAT Gateway A |
| Public B | `10.0.2.0/24` | Public resources, including NAT Gateway B |
| Private App A | `10.0.11.0/24` | Application instances |
| Private App B | `10.0.12.0/24` | Application instances |
| Private DB A | `10.0.21.0/24` | RDS primary placement in the diagram |
| Private DB B | `10.0.22.0/24` | RDS standby placement in the diagram |

## AWS services
- **VPC:** network isolation and subnet segmentation.
- **Route 53:** DNS resolution.
- **CloudFront:** content delivery and caching.
- **AWS WAF:** web request filtering.
- **Application Load Balancer:** distributes traffic to healthy targets.
- **EC2 Auto Scaling:** adjusts application capacity using target tracking.
- **Amazon RDS Multi-AZ:** primary/standby database availability design.
- **NAT Gateway:** outbound connectivity for private subnet resources.
- **Systems Manager Session Manager:** managed administrative access when configured.
- **CloudWatch and SNS:** monitoring, alarms, and notifications.

## Security considerations
- Keep application and database instances in private subnets.
- Apply least-privilege security-group rules.
- Allow database access only from the application security group.
- Use IAM roles for EC2 workloads.
- Do not commit credentials, private keys, passwords, tokens, or `.env` files.
- Validate WAF rules and encryption settings in the actual environment.

## Deployment details — complete only with verified values
| Item | Actual value |
|---|---|
| AWS Region | TODO |
| Application URL | TODO, if deployed |
| VPC ID | TODO |
| ALB DNS name | TODO |
| RDS engine/version | TODO |
| Auto Scaling min / desired / max | TODO |
| WAF Web ACL and rules | TODO |

## Evidence
Add genuine AWS console screenshots and test results for components actually deployed. Useful evidence includes VPC/subnets, route tables, NAT Gateways, ALB target health, Auto Scaling activity, RDS Multi-AZ status, CloudFront/WAF configuration, and CloudWatch/SNS alarms.

## Optional demonstration
If deployed, add a public application URL or a short demonstration video. Do not expose administrative interfaces or sensitive data.

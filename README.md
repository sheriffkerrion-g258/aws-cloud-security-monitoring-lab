# AWS Cloud Security Monitoring and Investigation Lab

## Project Overview

This project documents a hands-on investigation of AWS cloud security configurations using Amazon Web Services (AWS).

The objective was to understand how AWS CloudTrail records account activity and how EC2 Security Groups control inbound and outbound network traffic.

## Technologies Used

- AWS CloudTrail
- Amazon EC2
- EC2 Security Groups
- AWS Management Console

## Project Objectives

1. Investigate AWS management events using CloudTrail.
2. Examine EC2 security group permission changes.
3. Assess inbound SSH access.
4. Review outbound network permissions.
5. Identify potential security misconfigurations.
6. Document findings and remediation recommendations.

## Investigation 1: SSH Inbound Access

CloudTrail recorded an `AuthorizeSecurityGroupIngress` event.

Findings:
- Protocol: TCP
- Port: 22 (SSH)
- Source: A specific IPv4 address using a /32 CIDR.
- Result: The API operation succeeded.

Security assessment:

SSH access was restricted to one specified IPv4 address rather than being open to all IPv4 addresses.

## Investigation 2: Outbound Traffic

The security group allowed:

- Protocol: All
- Ports: All
- Destination: 0.0.0.0/0

Security assessment:

The rule permits unrestricted outbound IPv4 traffic. This is a potential security-hardening opportunity.

Recommendation:

Apply least-privilege outbound rules based on the actual requirements of the workload.

## Investigation 3: Resource Association

The security group had no EC2 instances associated with it when inspected.

It was identified as an unused resource and considered for cleanup.

## Key Lessons

- Understanding AWS CloudTrail management events.
- Investigating EC2 security group changes.
- Assessing inbound and outbound traffic permissions.
- Applying the principle of least privilege.
- Documenting cloud security findings.
- Identifying unused cloud resources.

## Scope and Limitations

This was a configuration investigation in my own AWS learning environment.

No IDS deployment, automated alerting, penetration testing, or confirmed threat detection was performed as part of this investigation.

## Evidence

See the `evidence/` directory for redacted screenshots of the investigation.

## Conclusion

This project strengthened my practical understanding of AWS cloud security, CloudTrail investigation, network access controls, and security configuration assessment.

## Automated Alerting Validation

### Objective
To verify that AWS CloudTrail, Amazon EventBridge, and Amazon SNS work together to detect and notify administrators about sensitive AWS configuration changes.

### Test Scenario
A controlled modification was made to an isolated EC2 Security Group to generate an `AuthorizeSecurityGroupIngress` API event.

### Event Details
- **AWS Service:** Amazon EC2
- **Event Name:** AuthorizeSecurityGroupIngress
- **Event Source:** aws.ec2
- **Event Detail Type:** AWS API Call via CloudTrail
- **AWS Region:** eu-north-1
- **Notification Service:** Amazon SNS

### Alert Pipeline

1. CloudTrail recorded the Security Group modification.
2. EventBridge received and matched the CloudTrail event.
3. EventBridge forwarded the matching event to the SNS topic.
4. SNS delivered an email notification.

### Result

**Status: Successful**

An email notification was successfully received after the controlled Security Group modification.

This confirmed that the end-to-end alerting pipeline was operational.

### Security Notes
- The test used an isolated Security Group.
- The test source was a documentation-only IP range.
- The test did not involve an actual attack or compromise.
- Sensitive AWS identifiers and personal information are excluded from published evidence.

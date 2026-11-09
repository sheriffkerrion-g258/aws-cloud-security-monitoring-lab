# Security Findings

## Finding 1: Broad Outbound Access

Resource: EC2 Security Group
Severity: Low to Medium (context-dependent)

Observation:
The security group allowed all outbound traffic to 0.0.0.0/0.

Potential Risk:
Unrestricted outbound connectivity may increase the impact
of a compromised instance.

Recommendation:
Restrict outbound traffic according to workload requirements.

## Finding 2: SSH Access

Observation:
Inbound SSH access was restricted to a specific IPv4 /32 address.

Assessment:
This is more restrictive than allowing SSH from 0.0.0.0/0.

Recommendation:
Continue restricting SSH access to trusted sources.

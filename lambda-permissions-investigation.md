# AWS Lambda Permissions Investigation

## Overview

Investigated an AWS CloudTrail event named
AddPermission20150331v2 to assess Lambda access permissions.

## Resource

Service: AWS Lambda
Function: CloudLearningFunction

## Observations

The CloudTrail event showed:

- Principal: *
- Action: lambda:InvokeFunctionUrl
- Function URL authentication: NONE
- Statement ID: FunctionURLAllowPublicAccess

## Security Finding

Public Lambda Function URL Invocation Permission.

The resource-based policy allowed any principal
to invoke the function URL without AWS IAM authentication.

## Potential Impact

Unauthenticated external callers could invoke the
function while the URL and permissions were active.

Potential consequences depend on the function's
implementation and include unexpected execution,
resource consumption, or unintended data exposure.

## Recommended Remediation

1. Prefer AWS_IAM authentication where appropriate.
2. Restrict invocation to trusted principals.
3. Apply least-privilege resource-based policies.
4. Review Lambda Function URL configurations.
5. Monitor permission changes using CloudTrail.

## Investigation Outcome

The Lambda function was subsequently deleted
during the learning exercise.

No evidence of unauthorized invocation was
established by this permission-change event alone.

## Technologies

- AWS Lambda
- AWS CloudTrail
- IAM Resource-Based Policies
- AWS Function URLs

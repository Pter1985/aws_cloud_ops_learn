# Managing Access

[[_TOC_]]

## IAM

Identity and Access Management

IAM controls who can access what by determining **who is authenticated** (logged in) and **authorized** (has permissions) to use your resources. It also helps meet compliance requirements by providing detailed control over resource access.

>[!IMPORTANT]
>**IAM is a global service.**

## AWS Resource access process

1. authenticating the user or application.
2. authorizing access requests.
3. granting permission to perform actions on AWS resources.

## Key components of IAM

- Users  
  A person or application that interacts with AWS.
- Groups  
  A collection of IAM users with similar access needs.
- IAM Role  
  A set of persmissions that users or services can assume.
- Policies  
  A JSON document that defines permissions by allowing or denying actions on specific resources.

## Unique user types

- Root user  
  Primary account holder with full access to all resources. This user should be used minimally because of its extensive permissions.
- Federated user  
  A federated user accessess AWS resources by authenticating outside AWS through an external Identity Provider (IdP)

## IAM Policies

IAM policies are written in JSON format.  
AWS first denies any request that is explicitly denied, allows requests that are explicitly allowed, and denies everything else by default.

## Policy elements

| Element   | Description                                                                                                                      | Required |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- | -------- |
| Effect    | Use Allow or Deny to indicatie whether the policy allows or denies access.                                                       | Yes      |
| Principal | Indicate the account, user, role, or federated user to which you would like to allow or deny access (only on resource policies). | No       |
| Action    | Include a list of actions that the policy allows or denies.                                                                      | Yes      |
| Resource  | Specify a list of resources to which the actions apply.                                                                          | Yes      |
| Condition | Specify the circumstances under which the policy grants permission.                                                              | No       |

### Example policy

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": "ec2:DescribeInstances",
     "Resource": "*"
   }
 ]
}
```

## policy types

| Policy type             | Description                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Identity-based policies | Attach managed and inline policies to IAM identities (users, groups to which users belong, and roles).                                                                                                                                                                                                                                                                                                   |
| Resource-based policies | Attach inline policies to resources. The most common examples of resource-based policies are Amazon Simple Storage Service (Amazon S3) bucket policies and IAM role trust policies.                                                                                                                                                                                                                      |
| Organizational SCPs     | Use an AWS Organizations Service Control Policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU).                                                                                                                                                                                                                                              |
| ACLs                    | Use access control lists (ACLs) to control which principals in other accounts can access a resource to which the ACL is attached. ACLs are similar to resource-based policies, but they are not written in JSON. Their format depends on the service (XML for Amazon S3 and rule tables for network ACLs). They are stored directly with the resource they protect rather than as separate policy files. |

## Common access patterns using roles

- Temporary elevated access
- Service-to-service access
- Cross-account access
- Federated user access
- Programmatic access

### Federated access with IAM

![alt text](images/fad_access.png)  
*example*

## Implementing access paterns

### Same account service-to-service communication

When services communicate within a single AWS account, IAM provides two main approaches:

- **Access control with resource policies**  
  Attach permissions directly to resources for services that support resource-based policies (such as Amazon Simple Storage Service [Amazon S3], Amazon Simple Notification Service [Amazon SNS], and AWS Lambda). Please note that you always have to specify the principal elements in a resource-based policy, to indicate who will access the resource. 
- **Access control with service role**  
  Create IAM roles with the appropriate permissions that AWS services can assume to perform actions on other AWS services.

### Cross-account service-to-service communication access with resource policies

Cross-account access requires cooperation between both accounts:

- The resource account (containing the resource to be accessed) must grant permission to the service account (containing the service that needs access).
- The service in the service account must be configured to access the cross-account resource.

## Choosing between cross-account approaches

| Cross-Account Resource Policies                         | Cross-Account Role Assumption                        |
| ------------------------------------------------------- | ---------------------------------------------------- |
| Has a simpler implementation                            | Works with all AWS services                          |
| Provides direct access without role assumption          | Has more centralized permission management           |
| Works with only services that support resource policies | Provides temporary credentials with limited lifetime |
| Is good for granting specific permissions               | Is better for complex permission scenarios           |

## IAM Best Practices

Before you begin implementing IAM in your own environments, familiarize yourselves with these recommended best practices that will help you avoid common pitfalls and strengthen your security posture from day one.

- Protect your root account.
- Create individual IAM users.
- Use groups to assign permissions.
- Follow the principle of least privilege.
- Configure strong password policies.
- Regularly rotate credentials.
- Use multi-factor authentication.
- Monitor and audit access patterns.

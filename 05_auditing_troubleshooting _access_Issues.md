# Auditing and Troubleshooting Access Issues

[[TOC]]

## IAM Access Analyzer

IAM Access Analyzer informs you which resources in your account you are sharing with external principals. It does this by using logic-based reasoning to analyze resource-based policies in your AWS environment. When you enable IAM Access Analyzer, you create an analyzer for your account. Your account is the zone of trust for the analyzer. The analyzer monitors all the supported resources within your zone of trust. Any access to resources by principals that are within your zone of trust are considered trusted.

There are two type of analyzers

- External Access
- Unused Access

## Functions of the IAM Analyzer

- External Access Identification
- Cross-Account access governance
- Unused Access identification
- Policy validation before deployment
- Continuous monitoring
- IAM Policy generation based on IAM users and roles access activity


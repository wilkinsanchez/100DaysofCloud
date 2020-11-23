![placeholder image](https://i0.wp.com/blog.ahasayen.com/wp-content/uploads/2018/09/Microsoft-Azure-PIM-2.png?resize=1080%2C609&ssl=1)

# Configured Azure AD Privileged Identity Management

## Introduction

Privileged Identity Management (PIM) is a service in Azure Active Directory (Azure AD) that enables you to manage, control, and monitor access to important resources in your organization. These resources include resources in Azure AD, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune.

## Use Case

Organizations want to minimize the number of people who have access to secure information or resources because that reduces the chance of a malicious actor getting that access, or an authorized user inadvertently impacting a sensitive resource. However, users still need to carry out privileged operations in Azure AD, Azure, Microsoft 365, or SaaS apps. Organizations can give users just-in-time privileged access to Azure resources and Azure AD. There is a need for oversight for what those users are doing with their administrator privileges.

## What does it do?

Privileged Identity Management provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about. Here are some of the key features of Privileged Identity Management:

* Provide just-in-time privileged access to Azure AD and Azure resources
* Assign time-bound access to resources using start and end dates
* Require approval to activate privileged roles
* Enforce multi-factor authentication to activate any role
* Use justification to understand why users activate
* Get notifications when privileged roles are activated
* Conduct access reviews to ensure users still need roles
* Download audit history for internal or external audit

## Cloud Research

For this lab, I worked on enabling PIM and configured assignments. From the user perspective, requested permissions for an Administrator task that needed 4 hours to complete.

## Social Proof

[LinkedIn](link)

![placeholder image](https://i0.wp.com/msexperttalk.com/wp-content/uploads/2019/08/082719_0405_AzureADCond1.png?ssl=1)

# Configure Conditional Access policy

## Introduction

Conditional Access policies at their simplest are if-then statements, if a user wants to access a resource, then they must complete an action. Example: A payroll manager wants to access the payroll application and is required to perform multi-factor authentication to access it.

## Use Case

Some use cases for Conditional Access are:

* Requiring multi-factor authentication for users with administrative roles
* Requiring multi-factor authentication for Azure management tasks
* Blocking sign-ins for users attempting to use legacy authentication protocols
* Requiring trusted locations for Azure AD Multi-Factor Authentication registration
* Blocking or granting access from specific locations
* Blocking risky sign-in behaviors
* Requiring organization-managed devices for specific applications

## Cloud Research

During this lab I created a policy that enables Multi-Factor Authentication when accessing the Azure Admin portal. I was able to deploy the policy to only a handful of users to make sure it works as expected.

https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/concept-conditional-access-policy-common
https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview

## Social Proof

[LinkedIn](link)

![placeholder image](https://www.devopspertise.com/wp-content/uploads/2020/06/arm-policy-resource-lock-title.png)

# Protect Azure Resources with Resource Manager Locks

## Introduction

As an administrator, you can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources. The lock overrides any permissions the user might have.

You can set the lock level to CanNotDelete or ReadOnly. In the portal, the locks are called Delete and Read-only respectively.

* CanNotDelete means authorized users can still read and modify a resource, but they can't delete the resource.

* ReadOnly means authorized users can read a resource, but they can't delete or update the resource. Applying this lock is similar to restricting all authorized users to the permissions granted by the Reader role.

To create or delete management locks, you must have access to Microsoft.Authorization/* or Microsoft.Authorization/locks/* actions. Of the built-in roles, only Owner and User Access Administrator are granted those actions.

## Cloud Research

During this lab I worked on setting up Azure locks to protect the most important resources of my cloud environment. With Azure locks we can prevent accidental deletion of important cloud resources for example.

## Resources

https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources



## Social Proof

[LinkedIn](https://www.linkedin.com/posts/wilkinsanchez_100daysofcloud-azurepolicy-azure-activity-6762731397917618176-nHVg)

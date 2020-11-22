![placeholder image](https://docs.microsoft.com/en-us/azure/role-based-access-control/media/overview/rbac-overview.png)

# Azure RBAC Roles

## Introduction

### What is Azure role-based access control (Azure RBAC)?

Azure RBAC is an authorization system built on Azure Resource Manager that provides fine-grained access management of Azure resources. Access management for cloud resources is a critical function for any organization that is using the cloud. Azure role-based access control (Azure RBAC) helps you manage who has access to Azure resources, what they can do with those resources, and what areas they have access to.

### What can I do with Azure RBAC?

Here are some examples of what you can do with Azure RBAC:

* Allow one user to manage virtual machines in a subscription and another user to manage virtual networks
* Allow a DBA group to manage SQL databases in a subscription
* Allow a user to manage all resources in a resource group, such as virtual machines, websites, and subnets
* Allow an application to access all resources in a resource group
* Azure includes several built-in roles that you can use. For example, the Virtual Machine Contributor role allows a user to create and manage virtual machines. If the built-in * roles don't meet the specific needs of your organization, you can create your own Azure custom roles.

## Use Case

RBAC gives you granular control over resource access. You could use it, for example, to:

* Give a user full ownership access to all the resources within a specific resource group
* Let a user manage access to all virtual machines in a subscription
* Give an application permission to manage a specific resource type within a specific resource group
* When you assign someone a role, that role becomes tied to their credentials and applies anywhere those credentials are used.

## Cloud Research

For today's lab, I created a custom RBAC role that allows members of a security group to have Read-Only permissions to the VM's deployed in my tenant. This is a great way of providing just the necessary set of permissions to users and you also have the flexibility to be very granular when setting it up.

https://sharegate.com/blog/azure-governance-best-practices-what-is-rbac
https://docs.microsoft.com/en-us/azure/role-based-access-control/overview

## Social Proof

[LinkedIn](link)

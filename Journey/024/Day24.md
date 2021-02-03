![placeholder image](https://azure.microsoft.com/svghandler/azure-policy?width=600&height=315)

# Manage Azure Policy

## Introduction

Azure Policy helps to enforce organizational standards and to assess compliance at-scale. Through its compliance dashboard, it provides an aggregated view to evaluate the overall state of the environment, with the ability to drill down to the per-resource, per-policy granularity. It also helps to bring your resources to compliance through bulk remediation for existing resources and automatic remediation for new resources.

Azure Policy allows you to ensure that all resources are configured with required services, and will tell you when systems are out of compliance. So if you want all of your resources to be configured with Azure Backups, for example, it will either alert you when a VM doesn’t have Azure Backups configured or can automatically configure Azure Backups on that VM.

## Use Case

Business rules for handling non-compliant resources vary widely between organizations. Examples of how an organization wants the platform to respond to a non-compliant resource include:

* Deny the resource change
* Log the change to the resource
* Alter the resource before the change
* Alter the resource after the change
* Deploy related compliant resources

Also, you can use some of the following built-in Azure Policy policies to follow your company compliance guidelines:

* <b>Allowed Storage Account SKUs (Deny):</b> Determines if a storage account being deployed is within a set of SKU sizes. Its effect is to deny all storage accounts that don't adhere to the set of defined SKU sizes.

* <b>Allowed Resource Type (Deny)</b>: Defines the resource types that you can deploy. Its effect is to deny all resources that aren't part of this defined list.

* <b>Allowed Locations (Deny):</b> Restricts the available locations for new resources. Its effect is used to enforce your geo-compliance requirements.

* <b>Allowed Virtual Machine SKUs (Deny):</b> Specifies a set of virtual machine SKUs that you can deploy.

* <b>Add a tag to resources (Modify):</b> Applies a required tag and its default value if it's not specified by the deploy request.

* <b>Not allowed resource types (Deny):</b> Prevents a list of resource types from being deployed.

## Cloud Research

During this lab I performed proof of concept using Azure Policy and performed the following tasks:

* Created an Azure resource group
* Created an allowed locations policy assignment with the following information
    * Only resources can be deployed in the East US availability zone
    * Prevent resources from getting created if they don't comply with this policy
* Tested my policy to make sure it works fine. To test it out, I tried deploying a virtual network to the East US availability zone and the UK West region to see the outcomes. As a result, I was able able to deploy the Virtual network on the East US zone.

## Social Proof

[LinkedIn](https://www.linkedin.com/posts/wilkinsanchez_wilkinsanchez100daysofcloud-activity-6762206813871050752-Z4Y4)

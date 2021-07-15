![placeholder image](https://www.edureka.co/blog/wp-content/uploads/2017/08/Virtual-Networks-Azure-Virtual-Networks-Edureka.png)

# Creating an Azure Virtual Network

## Introduction

During this lab I learned how to create an Azure Virtual Network with Subnets and network security groups. Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. VNet is similar to a traditional network that you'd operate in your own data center, but brings with it additional benefits of Azure's infrastructure such as scale, availability, and isolation.

## Use Case

Azure virtual network enables Azure resources to securely communicate with each other, the internet, and on-premises networks. Key scenarios that you can accomplish with a virtual network include - communication of Azure resources with the internet, communication between Azure resources, communication with on-premises resources, filtering network traffic, routing network traffic, and integration with Azure services.

## Cloud Research

Azure resources communicate securely with each other in one of the following ways:

* Through a virtual network: You can deploy VMs, and several other types of Azure resources to a virtual network, such as Azure App Service Environments, the Azure Kubernetes Service (AKS), and Azure Virtual Machine Scale Sets.
* Through a virtual network service endpoint: Extend your virtual network private address space and the identity of your virtual network to Azure service resources, such as Azure Storage accounts and Azure SQL Database, over a direct connection. Service endpoints allow you to secure your critical Azure service resources to only a virtual network.
* Through VNet Peering: You can connect virtual networks to each other, enabling resources in either virtual network to communicate with each other, using virtual network peering. The virtual networks you connect can be in the same, or different, Azure regions.

## ☁️ Cloud Outcome

During this lab I accomplished the following:

* Created a Virtual Network and a primary subnet
* Created a second Subnet
* Created a new Network Security Group and attached to primary subnet
* Attached security group to the Secondary Subnet

## Social Proof

[LinkedIn](link)

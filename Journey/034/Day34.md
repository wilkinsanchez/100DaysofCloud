![placeholder image](https://www.edureka.co/blog/wp-content/uploads/2017/08/Virtual-Networks-Azure-Virtual-Networks-Edureka.png)

# Deploying an Azure Virtual Network and Subnets using Terraform

## Introduction

During this lab I will be working on deploying an Azure Virtual Network and Subnets using Terraform.

Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. VNet is similar to a traditional network that you'd operate in your own data center, but brings with it additional benefits of Azure's infrastructure such as scale, availability, and isolation.

A subnet is a range of IP addresses in the VNet. You can divide a VNet into multiple subnets for organization and security. Each NIC in a VM is connected to one subnet in one VNet. NICs connected to subnets (same or different) within a VNet can communicate with each other without any extra configuration.

When you set up a VNet, you specify the topology, including the available address spaces and subnets. If the VNet is to be connected to other VNets or on-premises networks, you must select address ranges that don't overlap. The IP addresses are private and can't be accessed from the Internet, which was true only for the non-routable IP addresses such as 10.0.0.0/8, 172.16.0.0/12, or 192.168.0.0/16. Now, Azure treats any address range as part of the private VNet IP address space that is only reachable within the VNet, within interconnected VNets, and from your on-premises location.

## Lets get hands on!

### Step 1 — Access the Azure CLI

![image](https://user-images.githubusercontent.com/40305588/126103038-b569caac-4849-4d20-9093-414c4f700a33.png)

### Step 1 — Let's create a .tf file that will hold our Terraform code to deploy the resources we want

![image](https://user-images.githubusercontent.com/40305588/126418889-f9c4fa5b-3075-4219-8308-124ea13102e6.png)

### Step 3 — I used the following code to deploy the Azure VNEt and Subnets

```tf

provider "azurerm" {
    version = 1.38
    }

# Create virtual network
resource "azurerm_virtual_network" "Network_16" {
    name                = "LabVnet"
    address_space       = ["10.0.0.0/16"]
    location            = "eastus"
    resource_group_name = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"

    tags = {
        environment = "Terraform Networking"
        technician = "Wilkin Sanchez"
    }
}

# Create Sales subnet
resource "azurerm_subnet" "SalesSub" {
    name                 = "SalesSubnet"
    resource_group_name = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
    virtual_network_name = azurerm_virtual_network.Network_16.name
    address_prefix       = "10.0.1.0/24"
}

# Create HR Subnet
resource "azurerm_subnet" "HRSub" {
    name                 = "HRSubnet"
    resource_group_name = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
    virtual_network_name = azurerm_virtual_network.Network_16.name
    address_prefix       = "10.0.2.0/24"
}
```

### Step 4 - Run the following Terraform commands to deploy the changes

#### First command (terraform init)
![image](https://user-images.githubusercontent.com/40305588/126103633-e9a77097-6a46-4a86-8e57-80f102a9409e.png)

- The terraform init command is used to initialize a working directory containing Terraform configuration files. This is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control. It is safe to run this command multiple times.

#### Second command (terraform plan)
![image](https://user-images.githubusercontent.com/40305588/126103829-f059656c-126f-4f72-98ba-5a7ba9f1aa5a.png)

The terraform plan command creates an execution plan. By default, creating a plan consists of:
* Reading the current state of any already-existing remote objects to make sure that the Terraform state is up-to-date.
* Comparing the current configuration to the prior state and noting any differences.
* Proposing a set of change actions that should, if applied, make the remote objects match the configuration.

It's good to mention that it's a good idea to ALWAYS! run the "terraform plan" command before "terraform apply" so you have an idea of what will be added, changed, or destroyed.

#### Third command (terraform apply)
![image](https://user-images.githubusercontent.com/40305588/126103946-f63130c1-6465-4625-9be2-53dbe1027d53.png)

The terraform apply command executes the actions proposed in a Terraform plan. The most straightforward way to use terraform apply is to run it without any arguments at all, in which case it will automatically create a new execution plan (as if you had run terraform plan) and then prompt you to approve that plan, before taking the indicated actions.

### Verify that your changes were deployed to Azure

After deploying your Terraform configuration, make sure that the resources are showing up on the Azure portal. Be aware that it may take a few minutes for you to see those changes.

## ☁️ Cloud Outcome

During today's lab we accomplished the following:

* Researched about Terraform, Azure VNEt, and subnets.
* Configured an Azure VNEt and subnets.

## Resources

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview

## Social Proof

[link](link)

![placeholder image](https://i2.wp.com/build5nines.com/wp-content/uploads/2019/07/Azure_Network_Security_Groups_NSG_Featured_Image.jpg)

## Introduction

During this lab I will be working on deploying an Azure Virtual Network and Subnets using Terraform.

You can use an Azure network security group to filter network traffic to and from Azure resources in an Azure virtual network. A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources. For each rule, you can specify source and destination, port, and protocol.

### Security rules

|Property  |Explanation  |
|---------|---------|
|Name|A unique name within the network security group.|
|Priority | A number between 100 and 4096. Rules are processed in priority order, with lower numbers processed before higher numbers, because lower numbers have higher priority. Once traffic matches a rule, processing stops. As a result, any rules that exist with lower priorities (higher numbers) that have the same attributes as rules with higher priorities are not processed.|
|Source or destination| Any, or an individual IP address, classless inter-domain routing (CIDR) block (10.0.0.0/24, for example), service tag, or application security group. If you specify an address for an Azure resource, specify the private IP address assigned to the resource. Network security groups are processed after Azure translates a public IP address to a private IP address for inbound traffic, and before Azure translates a private IP address to a public IP address for outbound traffic. . Specifying a range, a service tag, or application security group, enables you to create fewer security rules. The ability to specify multiple individual IP addresses and ranges (you cannot specify multiple service tags or application groups) in a rule is referred to as [augmented security rules](#augmented-security-rules). Augmented security rules can only be created in network security groups created through the Resource Manager deployment model. You cannot specify multiple IP addresses and IP address ranges in network security groups created through the classic deployment model.|
|Protocol     | TCP, UDP, ICMP, ESP, AH, or Any.|
|Direction| Whether the rule applies to inbound, or outbound traffic.|
|Port range     |You can specify an individual or range of ports. For example, you could specify 80 or 10000-10005. Specifying ranges enables you to create fewer security rules. Augmented security rules can only be created in network security groups created through the Resource Manager deployment model. You cannot specify multiple ports or port ranges in the same security rule in network security groups created through the classic deployment model.   |
|Action     | Allow or deny        |

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

resource "azurerm_network_security_group" "nsg" {
  name                = "LabNSG"
  location            = "East US"
  resource_group_name = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
}

resource "azurerm_network_security_rule" "Port80Inbound" {
  name                        = "Web80"
  priority                    = 1001
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "80"
  destination_port_range      = "80"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
  network_security_group_name = azurerm_network_security_group.nsg.name
}

resource "azurerm_network_security_rule" "Port8080Inbound" {
  name                        = "Web8080"
  priority                    = 1000
  direction                   = "Inbound"
  access                      = "Deny"
  protocol                    = "Tcp"
  source_port_range           = "8080"
  destination_port_range      = "8080"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
  network_security_group_name = azurerm_network_security_group.nsg.name
}

  resource "azurerm_network_security_rule" "Port22Inbound" {
  name                        = "SSH"
  priority                    = 1100
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "*"
  destination_port_range      = "22"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
  network_security_group_name = azurerm_network_security_group.nsg.name
}

  resource "azurerm_network_security_rule" "Port80Outbound" {
  name                        = "Web80Out"
  priority                    = 1000
  direction                   = "Outbound"
  access                      = "Deny"
  protocol                    = "Tcp"
  source_port_range           = "80"
  destination_port_range      = "80"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = "155-20e5ee2a-deploy-azure-vlans-and-subnets-with-t"
  network_security_group_name = azurerm_network_security_group.nsg.name
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

An interesting use case of Terraform and Network Security Groups is the management of network rules priority. Imagine you have hundreds/thousands of network rules, and you will have to modify a handful of them. If you use the Azure portal, you will need to remove the rule and create it from scratch. With Terraform you can just update the line of code that handle the priority on the rule you are modifying, and deploy. After that, your changes will get applied without having to manually re-create the rule.

During today's lab we accomplished the following:

* Continued researching about Terraform, Azure Network Security Groups.
* Created an Azure Network Security Group with Terraform.

## Resources

https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview

## Social Proof

[link](link)

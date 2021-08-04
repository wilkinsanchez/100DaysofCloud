![placeholder image](https://i0.wp.com/build5nines.com/wp-content/uploads/2020/04/Terraform_on_Azure_Featured_Image_1.jpg?fit=1200%2C675&ssl=1)

# Deploying an Azure VM with networking using Terraform

## Introduction

During this lab I worked on deploying an Azure VM with networking information using Terraform.

## Lets get hands on!

### Step 1 — Access the Azure CLI

![image](https://user-images.githubusercontent.com/40305588/126103038-b569caac-4849-4d20-9093-414c4f700a33.png)

### Step 1 — Let's create a .tf file that will hold our Terraform code to deploy the resources we want

![image](https://user-images.githubusercontent.com/40305588/126418889-f9c4fa5b-3075-4219-8308-124ea13102e6.png)

### Step 3 — I used the following code to deploy the Azure VM, VNET, Subnet, Public IP, NIC, and Boot Diagnostics account

```tf

provider "azurerm" {
    version = 1.38
    }

# Create virtual network
resource "azurerm_virtual_network" "TFNet" {
    name                = "tfvmnetwork"
    address_space       = ["10.0.0.0/16"]
    location            = "East US"
    resource_group_name = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"

    tags = {
        environment = "Terraform VNET"
        technician = "Wilkin Sanchez"
    }
}
# Create subnet
resource "azurerm_subnet" "tfsubnet" {
    name                 = "default"
    resource_group_name = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"
    virtual_network_name = azurerm_virtual_network.TFNet.name
    address_prefix       = "10.0.1.0/24"
}

#Deploy Public IP
resource "azurerm_public_ip" "publiciptf" {
  name                = "pubip1"
  location            = "East US"
  resource_group_name = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"
  allocation_method   = "Dynamic"
  sku                 = "Basic"
}

#Create NIC
resource "azurerm_network_interface" "publiciptf" {
  name                = "tfvmnic"
  location            = "East US"
  resource_group_name = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"

    ip_configuration {
    name                          = "ipconfig1"
    subnet_id                     = azurerm_subnet.tfsubnet.id
    private_ip_address_allocation  = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.publiciptf.id
  }
}

#Create Boot Diagnostic Account
resource "azurerm_storage_account" "sa" {
  name                     = "diagvmtf"
  resource_group_name      = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"
  location                 = "East US"
   account_tier            = "Standard"
   account_replication_type = "LRS"

   tags = {
    environment = "Boot Diagnostic Storage"
    CreatedBy = "Admin"
   }
  }

#Create Virtual Machine
resource "azurerm_virtual_machine" "publiciptf" {
  name                  = "robotvm"
  location              = "East US"
  resource_group_name   = "187-b3e5c54d-deploying-an-azure-vm-with-terraform"
  network_interface_ids = [azurerm_network_interface.publiciptf.id]
  vm_size               = "Standard_B1s"
  delete_os_disk_on_termination = true
  delete_data_disks_on_termination = true

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "16.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "osdisk1"
    disk_size_gb      = "128"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "robotvm01"
    admin_username = "vmadmin"
    admin_password = "Password12345!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }

boot_diagnostics {
        enabled     = "true"
        storage_uri = azurerm_storage_account.sa.primary_blob_endpoint
    }
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

## Cloud Outcome

During this lab I accomplished the following using Terraform:

* Deployed an Azure VM using
* Created a VNET
* Created a Subnet
* Deployed a Public IP
* Created a NIC
* Created a Boot Diagnostics Account

## Social Proof

[link](link)

![placeholder image](https://miro.medium.com/max/1119/1*5fXMv4u9Kf79ptJyI7qF3g.png)

# Deploying an Azure File Share and Blob Storage using Terraform

## Introduction

During this lab we will be working on deploying an Azure File Share and Blob Storage using Terraform.

An Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

## Lets get hands on!

### Step 1 — Access the Azure CLI

![image](https://user-images.githubusercontent.com/40305588/126103038-b569caac-4849-4d20-9093-414c4f700a33.png)

### Step 1 — Let's create a .tf file that will hold our Terraform code to deploy the resources we want

![image](https://user-images.githubusercontent.com/40305588/126418889-f9c4fa5b-3075-4219-8308-124ea13102e6.png)

### Step 3 — I used the following code to deploy the Azure Storage Account

```tf

provider "azurerm" {
    version = 1.38
    }
    
resource "azurerm_storage_account" "lab" {
  name                     = "newshareandbloblab"
  resource_group_name      = "183-0719d5ce-deploy-an-azure-file-share-with-terra"
  location                 = "eastus"
  account_tier             = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = "Terraform Storage Account"
    CreatedBy = "WilkinSanchez-Admin"
      }
}

resource "azurerm_storage_container" "lab" {
  name                  = "blobcontainerlab"
  storage_account_name  = azurerm_storage_account.lab.name
  container_access_type = "private"

}

resource "azurerm_storage_blob" "lab" {
  name                   = "TerraformBlob"
  storage_account_name   = azurerm_storage_account.lab.name
  storage_container_name = azurerm_storage_container.lab.name
  type                   = "Block"

}
resource "azurerm_storage_share" "lab" {
  name                 = "terraformshare"  
  storage_account_name = azurerm_storage_account.lab.name
  quota                = 40

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

* Researched about Terraform, Blob Storages, and Azure File Shares.
* Configured an Azure Storage Blob container and File Share with Terraform via the Azure CLI.

## Resources

https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction <br>
https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share?tabs=azure-portal <br>
https://www.terraform.io/docs/index.html

## Social Proof

[LinkedIn](link)

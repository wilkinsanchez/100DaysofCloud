![placeholder image](https://docs.microsoft.com/en-us/azure/mysql/media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

# Deploying a MySQL Database using Terraform

## Introduction

For today's lab I worked on deploying a MySQL database instance using Terraform. Azure Database for MySQL is a relational database service powered by the MySQL community edition.You can use either Single Server or Flexible Server (Preview) to host a MySQL database in Azure. It's a fully managed database as a service offering that can handle mission-critical workloads with predictable performance and dynamic scalability.
 
## Lets get hands on!

### Step 1 — Access the Azure CLI

![image](https://user-images.githubusercontent.com/40305588/126103038-b569caac-4849-4d20-9093-414c4f700a33.png)

### Step 1 — Let's create a .tf file that will hold our Terraform code to deploy the resources we want

![image](https://user-images.githubusercontent.com/40305588/126418889-f9c4fa5b-3075-4219-8308-124ea13102e6.png)

### Step 3 — I used the following code to deploy the SQL Instance

```tf

provider "azurerm" {
    version = 1.38
    }

resource "azurerm_mysql_server" "example1" {
  name                = "mysql-terraformserver-2"
  location            = "East US"
  resource_group_name = "186-e3df50ac-deploy-a-mariadb-database-with-terraf"

  sku {
    name     = "B_Gen5_2"
    capacity = 2
    tier     = "Basic"
    family   = "Gen5"
  }

  storage_profile {
    storage_mb            = 5120
    backup_retention_days = 7
    geo_redundant_backup  = "Disabled"
  }

  administrator_login          = "mysqladminun"
  administrator_login_password = "easytologin4once!" #Make sure to reset this password after Server is deployed.
  version                      = "5.7"
  ssl_enforcement              = "Enabled"
}

resource "azurerm_mysql_database" "example1" {
  name                = "exampledb"
  resource_group_name = "186-e3df50ac-deploy-a-mariadb-database-with-terraf"
  server_name         = azurerm_mysql_server.example1.name
  charset             = "utf8"
  collation           = "utf8_unicode_ci"
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

* Deployed an Azure MySQL server instance with a Gen5, 2cpu, and standard SKU using Terraform.

## Resources

https://docs.microsoft.com/en-us/azure/mysql/ <b>
https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/app_service

## Social Proof

[LinkedIn](link)

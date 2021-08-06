![placeholder image](https://azure.microsoft.com/images/page/services/app-service/index/benefit-2.png?v=28c34f5e4f3e1083bf7bf30d324019c9a55eb0511349c21f5b068d01419662c9)

# Deploying Azure Web Apps using Terraform

## Introduction

For today's lab I will be deploying an Azure Application Service plan with a .NET Framework site with a Local Git content management setting. If you are working with a DevOps team, you may encounter many requests to either set up a Web app or provide the DevOps team with a way to deploy their own. By deploying the application with Terraform, you can set guidelines for naming conventions, code repo's, service plan levels, and deployment locations.

Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. You can develop in your favorite language, be it .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python. Applications run and scale with ease on both Windows and Linux-based environments.

App Service not only adds the power of Microsoft Azure to your application, such as security, load balancing, autoscaling, and automated management. You can also take advantage of its DevOps capabilities, such as continuous deployment from Azure DevOps, GitHub, Docker Hub, and other sources, package management, staging environments, custom domain, and TLS/SSL certificates.

With App Service, you pay for the Azure compute resources you use. The compute resources you use are determined by the App Service plan that you run your apps on.

## Lets get hands on!

### Step 1 — Access the Azure CLI

![image](https://user-images.githubusercontent.com/40305588/126103038-b569caac-4849-4d20-9093-414c4f700a33.png)

### Step 1 — Let's create a .tf file that will hold our Terraform code to deploy the resources we want

![image](https://user-images.githubusercontent.com/40305588/126418889-f9c4fa5b-3075-4219-8308-124ea13102e6.png)

### Step 3 — I used the following code to deploy the Web App

```tf

provider "azurerm" {
    version = 1.38
    }

resource "azurerm_app_service_plan" "svcplan" {
  name                = "newweb-appserviceplantf"
  location            = "eastus"
  resource_group_name = "191-238c2054-deploy-a-web-application-with-terrafo"

  tags = {
    environment = "Terraform Web App"
    technician = "Wilkin Sanchez"
  }
  sku {
    tier = "Standard"
    size = "S1"
  }
}

resource "azurerm_app_service" "appsvc" {
  name                = "custom-webapp-for-students-tf"
  location            = "eastus"
  resource_group_name = "191-238c2054-deploy-a-web-application-with-terrafo"
  app_service_plan_id = azurerm_app_service_plan.svcplan.id


  site_config {
    dotnet_framework_version = "v4.0"
    scm_type                 = "LocalGit"
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
## ☁️ Cloud Outcome

* Deployed an Azure App Service Plan with a .NET Framework site with Local Git content management settings.

## Resources

https://docs.microsoft.com/en-us/azure/app-service/overview <b>
https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/app_service

## Social Proof

[LinkedIn](https://www.linkedin.com/posts/wilkinsanchez_github-wilkinsanchez100daysofcloud-wilkins-activity-6829238366559719424-EZgY)

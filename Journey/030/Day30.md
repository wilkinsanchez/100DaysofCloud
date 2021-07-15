![placeholder image](https://www.pei.com/wp-content/uploads/2017/06/Azure-Backup.png)

# Backing up an Azure VM using Azure Backup Service

## Introduction

During this lab I learned about the Azure Backup service and how we can backup a VM in Azure. The Azure Backup service provides simple, secure, and cost-effective solutions to back up your data and recover it from the Microsoft Azure cloud. This is a great service that helps organizations restore data in case they get a ransomware on specific VM's for example.

## Use Case

* Simplify workload protection with built-in backup capabilities and save time with one-click backup support for VMs, Azure file shares, SQL and SAP HANA databases, and Azure Database for PostgreSQL.
* Manage resources through the Azure portal, Azure SDK, and Azure CLI, and across vaults, subscriptions, and tenants.
* Ensure database-consistent snapshots for Oracle and MySQL databases running on Linux VMs in Azure.

## Cloud Research

### What can I backup?

* On-premises - Back up files, folders, system state using the Microsoft Azure Recovery Services (MARS) agent. Or use the DPM or Azure Backup Server (MABS) agent to protect on-premises VMs (Hyper-V and VMware) and other on-premises workloads
* Azure VMs - Back up entire Windows/Linux VMs (using backup extensions) or back up files, folders, and system state using the MARS agent.
* Azure Managed Disks - Back up Azure Managed Disks
* Azure Files shares - Back up Azure File shares to a storage account
* SQL Server in Azure VMs - Back up SQL Server databases running on Azure VMs
* SAP HANA databases in Azure VMs - Backup SAP HANA databases running on Azure VMs
* Azure Database for PostgreSQL servers (preview) - Back up Azure PostgreSQL databases and retain the backups for up to 10 years
* Azure Blobs (preview) - Overview of operational backup for Azure Blobs (in preview)

## ☁️ Cloud Outcome

During this lab I accomplished the following:

* Created a VM
* Created a Recovery Services Vault
* Created a Backup Policy
* Enabled Backups and assigned backup policy to a VM.

## Social Proof

[link](link)

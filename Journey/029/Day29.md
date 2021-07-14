![placeholder image](https://cran.r-project.org/web/packages/AzureVM/readme/man/figures/logo.png)

# Using Powershell to resize an Azure VM in an Availability Set

## Introduction

During this lab we will work on resizing an Azure VM in an availability set. It's very important to learn how to do that because we could save money every if we are not using all the resources allocated to the VM. For example, reducing the CPU that's assigned to the VM.

## Use Case

Imagine that your company's Finance department says that the cost of the Azure VM's is getting over budget. So, what do we do? We have to find a way to decrease the cost of Azure VMs in the subscription. An easy solution would be to identify which VMs have low CPU utilization and change their size.


### Step 1 — Find the current size of the VMs

```powershell
Get-AzVM
```

### Step 2 — Get the VM Subscription names

```powershell
Get-AzSubscription
```

### Step 3 — Check VM CPU metrics. Replace <ID> with the VM Subscription name, <RESOURCE_GROUP_NAME> with the resource group name, and <VM> with the name of the Virtual machine you are checking the metrics

```powershell
az monitor metrics list --resource /subscriptions/<ID>/resourceGroups/<RESOURCE_GROUP_NAME>/providers/Microsoft.Compute/virtualMachines/<VM>
```
  
### Step 4 - Assign information of VM to variable (Resource Group Name and name of Virtual Machine we are resizing)

```powershell
$vm = Get-AzVM -ResourceGroupName <RESOURCE_GROUP_NAME> -VMName <VM>
```
### Step 5 - Complete the resize of the VMs:
  
  ```powershell
  $vm.HardwareProfile.VmSize = "Standard_B1s"
  Update-AzVM -VM $vm -ResourceGroupName <RESOURCE_GROUP_NAME>
  ```
For this particular example we are resizing the VM to the Standard_B1s. Find a list of more VM sizes here https://docs.microsoft.com/en-us/azure/virtual-machines/sizes-b-series-burstable
  
### Step 6 - Verify that the resize worked
  
  ```powershell
  Get-AzVM
  ```
  
At this point, you should be able to see the new size of your VM
  
## Social Proof

✍️ Show that you shared your process on Twitter or LinkedIn

[link](link)

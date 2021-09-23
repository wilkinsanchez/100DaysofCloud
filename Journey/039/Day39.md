![placeholder image](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/media/tshoot-connect-sync-errors/export_errors_overview_01.png)

# Troubleshoot sync issues between MS365 Cloud-only account and On-premises AD account

## Introduction

A few days I was troubleshooting an issue between an MS365 cloud-only account and an on-premises AD account that I found very interesting. A cloud email account was created for an user and I had to merge it with an on-prem AD account so the passwords are synced and the user doesn’t have to manage two different passwords.

It seems another admin created the cloud-only account not knowing their environment was AD Sync. The user had around 2gb of emails stored, so deleting the cloud-only account wasn’t the best option. Also, you can’t sync an AD account with the same email, it would create a sync issue. Therefore, the AD account the user was using on a daily basis to access her computer was being synced to MS365 as user@whateverdomain.onmicrosoft.com.

I was investigating what was the best way to accomplish that with the  minimal user impact/downtime. Someone recommended to

1. Convert the cloud-only mailbox to a shared mailbox
2. Migrate emails and such to another mailbox
3. Recreate mailbox from scratch

Too painful and time consuming!! So nooo!

What if I can merge the cloud-only account to the AD synced account without losing any of the emails and data? It’s possible if you hard match the immutable ID of the Cloud only and AD account using Powershell.

## Prerequisite

* Basic knowledge of MS365
* Basic knowledge of Powershell

### Step 1 — Access the servers that are running Active Directory and Azure AD Connect

Installing Azure AD Connect on a Domain Controller is not recommended due to security practices and more restrictive settings that can prevent Azure AD Connect from installing correctly.

Azure AD Connect must be installed on Windows Server 2008 R2 or later. This server must be domain joined and may be a domain controller or a member server.

### Step 2 — Keep note of the following information

* UPN of AD account you are troubleshooting.
* UPN of MS365 Cloud-Only account you would like to merge.

The UPN (User Principal Name) is basically the username of the accounts.

### Step 3 — Get information about AD User

Run the following Powershell command to get more information about the user you're troubleshooting

```powershell
Get-ADUser -Identity test
```
the "test" username will be the account you're troubleshooting.

### Step 4 — Find immutable ID of AD Account

The fun begins now! You will have to run the following command to convert the ObjectGUID of the user to base64.

```powershell
ldifde -f c:\exporttest.txt -r “(Userprincipalname=test@whateverupn.local)” -l “objectGuid, UserPrincipalName”
```

It will export a .txt file to the location specified containing the base64 Immutable ID that will be needed to hard match both accounts.

### Step 5 - Connect to MS365 tenant

We will connect to our MS365 tenant using Powershell. The commands are

```powershell
Import-Module MSOnline
Connect-MsolService
```

You will have to authenticate with an account that has Global Admin rights.

### Step 6 - Move AD Account to non-synced OU (Organizational Unit) within Active Directory

Next IMPORTANT thing you have to do is move the AD user you’re having issues with to a non-synced OU within Active Directory and run a Delta Sync.

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```
It will move the test@whateverdomain.onmicrosoft.com to the deleted users in MS365

### Step 7 - Remove AD synced account from MS-365

run the following command to remove that user from the recycle bin

```powershell
Remove-MsolUser -UserPrincipalName test@whateverdomain.onmicrosoft.com -RemoveFromRecycleBin -Force
```
Running this command guarantees that the AD Sync user gets removed from MS365 before merging.

### Step 8 - Let's hard match the Immutable ID's of both accounts

We are going to change the immutable ID of our cloud-only account to match our AD Sync account. Run the following

```powershell
Set-MsolUser -UserPrincipalName test@whateverdomain.com -ImmutableId “paste the base64 you generated here”
```
It will hard match it with the AD account.

### Step 9 - Move AD User to OU that's syncing

Now it’s time to move the AD user to an OU in AD that’s syncing to your MS365 tenant. After that, run another Delta sync

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```
It should take a few minutes and you should see the Cloud-only account changing its cloud icon to a server icon 

## Social Proof

✍️ Show that you shared your process on Twitter or LinkedIn

[link](link)

![placeholder image](https://www.solix.com/blog/wp-content/uploads/2020/03/email-archiving.jpeg)

# Configure In-Place archiving, retention tags, and policies

## Introduction

✍️ For today's lab I will work on configuring In-Place archiving, retention tags, and policies using the Microsoft 365 Compliance center. In-Place Archiving provides users with additional mailbox storage space. After you turn on archive mailboxes, users can access and store messages in their archive mailboxes by using Microsoft Outlook and Outlook on the web (formerly known as Outlook Web App). Users can also move or copy messages between their primary mailbox and their archive mailbox. They can also recover deleted items from the Recoverable Items folder in their archive mailbox by using the Recover Deleted Items tool.

## Use Case

Several users in the organization reported that their Mailboxes are getting full. As an Administrator, we need to make sure those users keep receiving/sending emails. We recommended the following:

* Enable In-Place archiving
* Configure Custom Retention Tags based on the user type and the organization policy
* Configure Custom Retention Policy that will get added to the users with their Mailbox full
* Force an update on their Archive Mailbox using Powershell.

## Cloud Research

This lab was very interesting because it allowed me to enable In-Place archiving, and create custom retention tags and policies. In the past, I would create a .PST archive, but that's not too efective because users can lose that file and consequently lose those emails. With this solution, the archived emails will stay on the cloud and the users can access them for as long as the emails are not deleted.

https://docs.microsoft.com/en-us/microsoft-365/compliance/enable-archive-mailboxes?view=o365-worldwide

## Social Proof

[LinkedIn](https://www.linkedin.com/posts/wilkinsanchez_wilkinsanchez100daysofcloud-activity-6790094673584226304-X3G1)

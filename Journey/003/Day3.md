<!-- This template removes the micro tutorial for a quicker post and removes images for a full template check out the 000-DAY-ARTICLE-LONG-TEMPLATE.MD-->

**Add a cover photo like:**
![placeholder image](https://www.managedsolution.com/wp-content/uploads/2018/09/bigstock-Password-Input-On-Blurred-Back-236308780-1920x1282.jpg)

# Deploy Azure AD Smart Lockout

## Introduction

I chose to work on this lab to understand how we can secure Azure AD accounts with smart lockout. Smart lockout helps lock out bad actors that try to guess your users' passwords or use brute-force methods to get in. Smart lockout can recognize sign-ins that come from valid users and treat them differently than ones of attackers and other unknown sources.

## Use Case

I wanted to secure my trial tenant as much as I could by making sure attackers can't bruteforce the passwords of my users. I set it so after 3 unsuccessful attempts the accounts get locked out. Also, I setup a Custom banned password list that doesn't allow users to create any of the passwords on the list.

## Cloud Research

I read some articles from Microsoft that allowed me to understand the technology behind Smart Lockout and how to implement it securely. I ran into some issues with the Custom password list, but it worked fine after a couple tries.

https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-password-smart-lockout
## Social Proof

[link](link)

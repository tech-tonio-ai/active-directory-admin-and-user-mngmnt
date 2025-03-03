<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Admin and User Management (Azure)</h1>
This project involves setting up Active Directory, creating domain admin and user accounts, and managing access within a secure domain environment. The goal is to ensure proper user management and secure access across systems using Active Directory services.

## Active Directory Domain Services
- Login to DC-1 and install Active Directory Domain Services
<p align="center">
  <img src="https://i.imgur.com/SWXkR0v.png" alt="Image 1" width="45%"/>  
</p>
- Promote as a DC: Setup a new forest as `mydomain.com` (can be anything, just remember what it is).
<p align="center">
  <img src="https://i.imgur.com/FUkZou6.png" alt="Image 1" width="45%"/>  
</p>
- Restart and then log back into DC-1 as user: `mydomain.com\labuser`.
<p align="center">
  <img src="https://i.imgur.com/TuI71lr.png" alt="Image 1" width="45%"/>  
</p>

## Create a Domain Admin user within the domain
- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and “_ADMINS”.
<p align="center">
  <img src="https://i.imgur.com/ZGOiKN2.png" alt="Image 1" width="45%"/>  
</p>
<p align="center">
  <img src="https://i.imgur.com/AsLUamo.png" alt="Image 1" width="45%"/>  
</p>
- Create a new employee named “Jane Doe” (same password) with the username of `jane_admin` / `Cyberlab123!`.
- Add `jane_admin` to the “Domain Admins” Security Group.
<p align="center">
  <img src="https://i.imgur.com/wySBSJt.png" alt="Image 1" width="45%"/>  
</p>
- Log out / close the connection to DC-1 and log back in as `mydomain.com\jane_admin`.
- Use `jane_admin` as your admin account from now on.
<p align="center">
  <img src="https://i.imgur.com/3sCjZaa.png" alt="Image 1" width="45%"/>  
</p>

## Join Client-1 to your domain (`mydomain.com`)
- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address (Already done).
- From the Azure Portal, restart Client-1 (Already done).
- Login to Client-1 as the original local admin (`labuser`) and <b>join</b> it to the domain (computer will restart).
- <p align="center">
  <img src="https://i.imgur.com/rqXWgw3.png" alt="Image 1" width="45%"/>  
</p>

- Login to the Domain Controller and verify Client-1 shows up in ADUC.
- Create a new OU named “_CLIENTS” and drag Client-1 into there.
<p align="center">
  <img src="https://i.imgur.com/Ao49Q38.png" alt="Image 1" width="45%"/>  
</p>

**Finish the lab**, but do not delete the VMs in Azure. We will use them for upcoming labs.
If you are done for the day and want to save money, simply “Stop”/turn off the VMs within the Azure Portal.

---

# Part 2

## Turn on the DC-1 and Client-1 VMs in the Azure Portal if they are off.

## Setup Remote Desktop for non-administrative users on Client-1
- Log into Client-1 as `mydomain.com\jane_admin`.
- Open system properties.
- Click “Remote Desktop”.
- Allow “domain users” access to remote desktop.
- You can now log into Client-1 as a normal, non-administrative user now.
- Normally, you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab).

## Create a list of additional users and attempt to log into Client-1 with one of the users
- Login to DC-1 as `jane_admin`.
- Open PowerShell ISE as an administrator.
- Create a new file and paste the contents of the [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it.
- Run the script and observe the accounts being created.
- When finished, open ADUC and observe the accounts in the appropriate OU (_EMPLOYEES).
- Attempt to log into Client-1 with one of the accounts (take note of the password in the script).


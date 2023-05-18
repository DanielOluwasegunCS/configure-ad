<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used</h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://imgur.com/tD2vkbm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I created a Windows Server 2022 virtual machine (VM) in Microsoft Azure and called it "DC-1". I also set DC-1's Network Interface Card (NIC) private IP address to be static.
</p>
<br />

<p>
<img src="https://imgur.com/H8x7edQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I created a Windows 10 VM and called it "Client-1". I used the same resource group and virtual network as DC-1's.
</p>
<br />

<p>
<img src="https://imgur.com/4WASrUq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I am logged into DC-1 and I installed Active Directory (AD) Domain Services.
</p>
<br />

<p>
<img src="https://imgur.com/9oH7ez1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I promoted AD to a Domain Controller (DC) and setup a new forest as "danielO.com."
</p>
<br />

<p>
<img src="https://imgur.com/UpKiuHI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Active Directory Users and Computers (ADUC), I created an Organizational Unit (OU) called "_EMPLOYEES" and an OU called "_ADMINS." I created a new employee named "Daniel Oluwasegun" with the username of "dan.admin." I added dan.admin to the "Domain Admins" Security Group. I then logged out of the Remote Desktop Connection to DC-1 and logged back in as "danielO.com\dan.admin."
</p>
<br />

<p>
<img src="https://imgur.com/ul09BtV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Azure Portal, I set Client-1’s DNS settings to DC-1’s Private IP address.
</p>
<br />

<p>
<img src="https://imgur.com/2cDHewh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I logged in to Client-1 as the original local admin (labuser) and joined it to the domain.
</p>
<br />

<p>
<img src="https://imgur.com/KVXR27v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I verified that Client-1 showed up in ADUC inside the "Computers" file on the root of the domain. I then created a new OU named "_CLIENTS" and dragged Client-1 into there.
</p>
<br />

<p>
<img src="https://imgur.com/x09Iv6Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here, I allowed "domain users" access to remote desktop so that I could log into Client-1 as a normal, non-administrative user.
</p>
<br />

<p>
<img src="https://imgur.com/BdhQvtz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I created a new file in PowerShell_ISE and pasted the contents of a script into it. The script makes a variable amount (can be changed) of user accounts with random vowels and consonants. The default password is "Password1" (can be changed). I ran and used this script in order to see if Client-1 could be logged into by a normal, non-administrative account.
</p>
<br />

<p>
<img src="https://imgur.com/PiJWXTQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In ADUC, I observed the accounts in the "_EMPLOYEES" OU.
</p>
<br />

<p>
<img src="https://imgur.com/A5ReKK3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I attempted to log into Client-1 with one of the accounts.
</p>
<br />

<p>
<img src="https://imgur.com/XsiHDNC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I went into cmd prompt just to verify if I was logged into as the non-admin account and if I was in the Client-1 VM.
</p>
<br />

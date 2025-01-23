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

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create several additional users & attempt to log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.gyazo.com/3aa82fecc8b145cc679638212577bd3b.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/e149cadb2d14f0ef3fb5c9401c261f16.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/acd5d1605eb7efc51f927aabdbac0864.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/3aa82fecc8b145cc679638212577bd3b.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
To begin, I logged into DC-1 and installed Active Directory Domain Services. During the promotion process, I set up a new forest with the domain name “mydomain.com.” After the promotion, I restarted the server and logged back in as “mydomain.com\labuser.”
</p>
<br />

<p>
<img src="https://i.gyazo.com/424aa6a6111cdf8f55d34588e15bd1be.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/abdaadca759899c2e66126b85d887117.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/21ae6d0de61d28220c58a57bb9521994.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/d59c8acc4d5c3358ab593dcdc273c28c.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/f18297f20ea3653f1961694f277abbd0.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Next, in Active Directory Users and Computers (ADUC), I created two Organizational Units (OUs): one named “_EMPLOYEES” and another called “_ADMINS.” I then created a new user, “Jane Doe,” with the username “jane_admin.” Following that, I added “jane_admin” to the “Domain Admins” Security Group. After logging out, I logged back in using the “mydomain.com\jane_admin” account.
</p>
<br />

<p>
<img src="https://i.gyazo.com/f18ef53c72578ea7412df8eb700c413a.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/aecab1054aa94080d58f3232414e6864.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/686d6bd90edd43f49ae5b8601d6a7fee.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/3aa82fecc8b145cc679638212577bd3b.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/390b644a236d191e45e64b7e10352158.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/70437f78ca7092e0742f9f7c4f976be8.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
In the Azure Portal, I configured Client-1’s DNS settings to point to the DC’s private IP address and restarted the machine. I then logged into Client-1 using the original local admin account, “labuser,” and joined the computer to the domain. I then logged into the Domain Controller and verified that Client-1 appeared in ADUC. I proceeded to create a new OU named “_CLIENTS” and moved Client-1 into it.
</p>
<br />

<p>
<img src="https://i.gyazo.com/2eb07119b18d8fa966d9aab966964b00.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
I logged into Client-1 as “mydomain.com\jane_admin,” opened the system properties, and enabled Remote Desktop access for “domain users.” This allowed normal, non-administrative users to log into Client-1. Ideally, this setting would be configured through Group Policy to apply across multiple systems at once.
</p>
<br />

<p>
<img src="https://i.gyazo.com/b04d09fd31c9d6439770daea630563d6.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/fc83569296840d1e9fc7ffc2e60cfb62.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/755c1b10c713e57d437f58634fa1e774.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/650ce247a0ed10f5ee4a220655f68a44.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
<img src="https://i.gyazo.com/5998533342177beb20791fe9780d23d5.jpg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Finally, I logged back into DC-1 as “jane_admin,” opened PowerShell_ise as an administrator, created a new file, and pasted the script into it. The script was designed to automate the creation of new user accounts. After running it, I observed the accounts being created successfully. Once the script finished, I opened ADUC to verify that the new accounts were listed in the “_EMPLOYEES” OU. To test, I attempted to log into Client-1 using one of the newly created accounts, confirming that it worked properly.
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to domain
- Setup Remote Desktop for non-administrative users on client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/SyvinMi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Domain Controller Virtual Machine (Windows Server 2022) named DC-1 and a Client Virtual Machine (Windows 10) named Client-1. Make sure both are created in the same Resource Group and Virtual Network. Set the Domain Controller's NIC Private IP Address to be static.
</p>
<br />
  
<p>
<img src="https://i.imgur.com/LaOiszY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ensure connectivity between the client and Domain Controller: Login to Cleint-1 with Remote Desktop, open Command Prompt, and ping DC-1's private IP address with "ping -t<IP address>. This will enable a perpetual ping. Login to the Domain Controller and enable ICMPv4 in the local Windows Firewall. Check back at Client-1 to see the ping succeed.
</p>
<br />

<p>
<img src="https://i.imgur.com/2qXyRHv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install Active Directory: Open Remote Desktop Connection and login to DC-1 with the credentials created in Microsoft Azure.
</p>
<br />

<p>
<img src="https://i.imgur.com/BMmnHU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside DC-1, open Server Manager and click on "Add Roles and Features"
</p>
<br />

<p>
<img src="https://i.imgur.com/dM10kNk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
when the installation window pops up, click next -> Ensure the destination Server is DC-1 and click next -> Check the Active Directory Domain Services box and click next. 
</p>
<br />

<p>
<img src="https://i.imgur.com/WNazZiH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the Active Directory box is checked, click next through the process and install
</p>
<br />

<p>
<img src="https://i.imgur.com/xROd33o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The installation is not quite done yet. Go back to the Server Manager window and navigate to the flag icon at the top right corner. Click on the flag and click on "Promote this server to a domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/XJgaJi9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select "Add new a forest" -> Set a domain name (my domain.com) -> Click next -> Create a password for Directory Service Restore Mode (DSRM) -> Click next through to the end. After the installation, the Virtual Machine will restart.
</p>
<br />

<p>
<img src="https://i.imgur.com/BuKRA2I.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login back to DC-1 as "mydomain.com\labuser"
</p>
<br />

<p>
<img src="https://i.imgur.com/8rzdBp6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open Active Directory. An easy way is to type "Active Directory Users and Computers" in the search box
</p>
<br />

<p>
<img src="https://i.imgur.com/xlxsjdS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two organizational Units (OU) called "_EMPLOYEES" and "_ADMINS": Right-click on "mydomain.com" -> New -> Organizational unit.
</p>
<br />

<p>
<img src="https://i.imgur.com/exCuYmJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create new Employee: Right-click on _ADMINS -> New -> User.
  Type in the name (Koby Charis) and create a username (koby.charis) for the employee. CLick next and set a password for the account.
</p>
<br />

<p>
<img src="https://i.imgur.com/9Ob7pvl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Add Employee (koby.charis) to "Domain Admins" Security Group: Open "_ADMINS" OU -> right-click on koby.charis and select properties. Click on "Member of" and type "Domain Admins" in the box. Click OK to add the employee to the Domain Admins group.
</p>
<br />

<p>
<img src="https://i.imgur.com/Qc4GpsF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Close Remote Desktop Connection and log back in as "mydomain.com\koby.charis"
</p>
<br />

<p>
<img src="https://i.imgur.com/MWSrxAX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Join Client-1 to your domain (my domain.com): From the Azure portal, set Client-1's DNS settings to the Domain Controller's Private IP Address and restart Client-1
</p>
<br />

<p>
<img src="https://i.imgur.com/F5pViAM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 with remote desktop connection as the original local admin (labuser) and join it to the domain. right click on the start menu -> settings -> rename this PC (advanced) -> change -> click on domain -> type in the domain name (mydomain.com) -> Enter the name and password of the domain admin we created previously(mydomain.com\koby.charis) to join the domain. Client-1 will restart.
</p>
<br />

<p>
<img src="https://i.imgur.com/xrjLl8Y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After Client-1 has restarted, Log in as the domain admin (koby.charis)
</p>
<br />

<p>
<img src="https://i.imgur.com/pgD9fcS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setup Remote Desktop for non-administrative users on client-1: Right-click on the start menu -> system -> Remote desktop -> click on "select users that can remotely access this PC"
</p>
<br />

<p>
<img src="https://i.imgur.com/DRwotlp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type "domain users" in the box -> click on "check names" and hit OK. now you can remotely log in to client-1 as a domain user.
</p>
<br />

<p>
<img src="https://i.imgur.com/M6H31zI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create additional users with Powershell_Ise and attempt to log into client-1 with one of the users: Login to DC-1 as domain admin (koby.charis) -> open Powershell_ise as an administrator -> create a new file -> run script to create new users
</p>
<br />

<p>
<img src="https://i.imgur.com/BMmnHU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside DC-1, open Server Manager and click on "Add Roles and Features"
</p>
<br />

<p>
<img src="https://i.imgur.com/BMmnHU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside DC-1, open Server Manager and click on "Add Roles and Features"
</p>
<br />

<p>
<img src="https://i.imgur.com/BMmnHU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside DC-1, open Server Manager and click on "Add Roles and Features"
</p>
<br />

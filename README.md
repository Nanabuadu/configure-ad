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
Install Active Directory_1: Open Remote Desktop Connection and login to DC-1 with the credentials created in Microsoft Azure.
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

<p>
<img src="https://i.imgur.com/BMmnHU1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside DC-1, open Server Manager and click on "Add Roles and Features"
</p>
<br />

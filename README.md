<p align="center">
<img src="https://i.imgur.com/JmgQ6ed.jpg" alt="Wireshark Logo"/>
</p>

<h1>Creating VMs in Azure and analyzing network protocols</h1>
This project illustrates how to setup both Windows and Linux VMs in Azure. We will also be using Wireshark to analyze network traffic. <br />

<!---
<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)
--->
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Wireshark

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)
- Ubuntu Server</b> 20.04 LTS


<h2>Creating VMs</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1) Since the osTicket instance is going to be hosted on a VM, we'll start with that first. For all intents and purposes, this could be done on any VM manager, but in this case we'll use Azure's Virtual Machine
  Service to host it. Start by going to "Virtual Machines" in your Azure dashboard and create an Windows 10 VM with version 21H2. The specs you pick are at your discretion. Remember to document the username and password you set during the creation process.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2) Next, connect to the VM using Remote Desktop Connection (RDC). RDC using the search bar. Once it is open, enter the public IP address (pictured above, it will be different from mine) for the VM and enter the credentials. Keep in mind, if you are running Windows 10 Home on your host system, RDC will not be available for you. The only other option would be to upgrade to Windows 10/11 Pro or use third party software.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3) 
</p>
<br />

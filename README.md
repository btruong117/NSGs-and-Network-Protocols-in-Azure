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

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Wireshark

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)
- Ubuntu Server</b> 20.04 LTS


<h2>Creating VMs</h2>

<p>
<img src="https://i.imgur.com/jUfBh5B.png" height="80%" width="80%" alt="Vnet settings"/>
</p>
<p>
1) This project assumes that you have already setup an Azure account and are running a Windows computer for your host computer. For this project, we're going to need two Virtual Machines hosted on Azure. One running Windows 10 and one running Ubuntu. On your Azure homepage select or search for "Virtual Machines" and click the "Create" button and select "Azure virtual machine" in the dropdown. Once you enter the creation menu, we will start creating the Windows 10 VM. Give it a descriptive name and let Azure autocreate the resource group. Choose an available Region and Zone. Choose Windows 10 Pro for the Image. The size is at your discretion. Create and document login credentials as this will allow us to acces the VM via RDP. 
</p>
<br />
<p>Proceed to the "networking" tab and ensure there is a vnet created. Azure should create a default vnet with 10.0.0.0/24 like the one pictured above. If the vnet is not automatically created or you would like to customize it, you can do so by going to "Create new" in "Virtual network" and can edit it to your liking. Once that is complete, click review + create in the bottom left. Once the process is validated, click create and wait for the Windows VM to finish deploying. **Note: it is important to wait for this VM to finish first so that when we create the 2nd VM, it has access to the correct Resource group and Vnet.</p>
<br />

<p>
<img src="https://i.imgur.com/mG8G0lX.png" height="80%" width="80%" alt="Ubuntu Settings"/>
</p>
<p>
2) Next we will create the Ubuntu VM. Again, navigate to Virtual machines, click the Create button, and name the VM. However, we will click on the resource group dropdown and select the same resource group from step one. Select your the same region and zone as the first VM as well. For image we will select, Ubuntu Server 20.04 and like before the size is at your discretion. 
</p>
<br />
<p>One important differenc between the two VMs is the way we access them. Unlike the Windows VM, we cannot access the Ubuntu VM via RDP due to the remote desktop service not being supported by Linux OS's. In fact, for the purpose of this lab, we will won't  need direct remote access to the  Ubuntu VM at all. We will instead access it through the Windows VM to create network traffic. For the time being all we need to do is to create credentials to login to the Ubuntu VM. Under Administrator account, find "Authentication type" and select password (pictured above). Create and document your credentials and navigate to the Network tab. Like the resource group, select the same vnet that was created in step 1. Click review + create and click create again once it is validated.</p>
<br />

<p>
<img src="https://i.imgur.com/JmOFhgw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3) 
</p>
<br />

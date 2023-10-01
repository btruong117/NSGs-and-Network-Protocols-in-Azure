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
- Linux Commands

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)
- Ubuntu Server</b> 20.04 LTS


<h2>Section 1: Creating VMs</h2>

<p>
<img src="https://i.imgur.com/71ZuF0b.png" height="80%" width="80%" alt="Vnet settings"/>
</p>
<p>
1) This project assumes that you have already setup an Azure account and are running a Windows computer for your host computer. For this project, we're going to need two Virtual Machines hosted on Azure. One running Windows 10 and one running Ubuntu. On your Azure homepage select or search for "Virtual Machines" and click the "Create" button and select "Azure virtual machine" in the dropdown. Once you enter the creation menu, we will start creating the Windows 10 VM. Give it a descriptive name and let Azure autocreate the resource group. Choose an available Region and Zone. Choose Windows 10 Pro for the Image. The size is at your discretion. Create and document login credentials as this will allow us to acces the VM via RDP. 
</p>
<br />
<p>Proceed to the "networking" tab and ensure there is a vnet created. Azure should create a default vnet with 10.0.0.0/24 like the one pictured above. If the vnet is not automatically created or you would like to customize it, you can do so by going to "Create new" in "Virtual network" and can edit it to your liking (Marked in the red rectangle). Once that is complete, click review + create in the bottom left. Once the process is validated, click create and wait for the Windows VM to finish deploying. **Note: it is important to wait for this VM to finish first so that when we create the 2nd VM, it has access to the correct Resource group and Vnet.</p>
<br />

<p>
<img src="https://i.imgur.com/lDvYeBG.png" height="80%" width="80%" alt="Ubuntu Settings"/>
</p>
<p>
2) Next we will create the Ubuntu VM. Again, navigate to Virtual machines, click the Create button, and name the VM. However, we will click on the resource group dropdown and select the same resource group from step one. Select your the same region and zone as the first VM as well. For image we will select, Ubuntu Server 20.04 and like before the size is at your discretion. 
</p>
<br />
<p>One important differenc between the two VMs is the way we access them. Unlike the Windows VM, we cannot access the Ubuntu VM via RDP due to the remote desktop service not being supported by Linux OS's. In fact, for the purpose of this lab, we will won't  need direct remote access to the  Ubuntu VM at all. We will instead access it through the Windows VM to create network traffic. For the time being all we need to do is to create credentials to login to the Ubuntu VM. Under Administrator account, find "Authentication type" and select password (pictured above). Create and document your credentials and navigate to the Network tab. Like the resource group, select the same vnet that was created in step 1. Click review + create and click create again once it is validated.</p>
<br />

<p>
<img src="https://i.imgur.com/Sex0B8y.png" height="80%" width="80%" alt="Ubuntu Private IP"/>
</p>
<p>
3) Once both VMs are created, go back to Virtual Machines and click on the Ubuntu VM. This will lead you a general information page for the VM. The thing we need to keep track of for the time being is the private IP address (marked above). Document it and now we are ready to proceed to the rest of the project.
</p>
<br />

<h2>Section 2: Connecting to the Windows Virtual Machine and Installing Wireshark</h2>

<p>
  <img src="https://i.imgur.com/x7dTRaG.png" height="60%" width="60%" alt = "RDP client">
</p>
<p>
  1) We are now ready to connect to the windows VM. On your host computer, click the search bar and type "Remote Desktop Connection" and click the app. Once it is open, we should see a box that has "Computer name" with a text field next to it (pictured). Enter the public IP address of the Windows VM where the computer name text field is and click connect. The VMs public IP can be found in the Virtual Machines menu in Azure. It should be between the Size and Disks columns in the menu. Once you connect, enter the login credentials created in Section 1. 
</p>

<p><img src="https://i.imgur.com/uFkeEuV.png" height="60%" width="60%" alt="Certifcate warning"></p>

<p>If a yellow warning box asks you to continue, click yes. The Remote desktop service will then take up our screen and we will see a new windows desktop appear shortly. **Note: There can be a few issues that can prevent an RDP connection from happening. These will be addressed at the end in the troubleshooting section.**</p>

<br />
<p><img src="https://i.imgur.com/aI0ONYd.png" height="45%" wdith="60%" alt = "Wireshark Main Screen"></p>
<p>
  2) Once we reach the Windows desktop, we'll need to install Wireshark to analyze network traffic. Open Microsoft edge on the desktop and go to <a href="https://www.wireshark.org/">here</a>. Choose the Windows x64 installer and download it. Once downloaded, double click the installer and follow the deafult options for everything. Once the installation is completed, it will either auto launch or we can go to the search bar and search for Wireshark. It should show the following(Pictured above). Click the ethernet section on the main screen and we can proceed to the next section.
</p>
<h2>Section 3: Creating and Analyzing Network Traffic</h2>
<br />

<h3>ICMP Traffic</h3>
<p>
  <img src="https://i.imgur.com/bJI9QXM.png" height="80%" width="80%" alt="ICMP Traffic">
</p>

<p>
The first type of traffic we are going to analyze is from the Internet Control Message Protocol(ICMP). This protocol is used to facilitate troubleshooting and diagnostic tools for network connectivity such the ping command. For this lab, open the windows command line and type ping (your Ubuntu VM's private IP) -t. The ping command sends ICMP packets to the target device. If the target device receives and replies back to the pinging machine, then we have network connectivity between the two devices. In this case, we are pinging from the Windows VM to the Ubuntu VM to see if the two are connected to each other. Normally, ping will send out 4 ICMP packets. However, we are using the -t flag which will create an endless ping.
</p>
<br />
<p>If you've opened up the ethernet capture in Wireshark, you should see a wide variety of different packets going through. Since we are only trying to observe ICMP traffic, we'll need to filter the traffic. Like the image above, type icmp in to the search bar near the top of the screen and press enter. Now, we will only see ICMP traffic between the two VMs. Notice how each line in the capture is a request from the Windows source IP to the Ubuntu Destination IP and alternates to a reply from the Ubuntu source IP to the Windows destination IP.</p>
<p>
  <img src="https://i.imgur.com/AKbGjk4.png" height="80%" width="80%">
</p>
<p>Ping is not restricted to just devices on your private network and can allow you to ping devices or entities on the internet. This can be helpful if you have connectivity between devices on your Local Area Network(LAN) but not to the internet. In the image, we've pinged 8.8.8.8 which is the public Google Domain Name System(DNS) server. Notice how we have the same request and reply back and forth. **Note: To end any command that doesn't stop in the command line, click inside the cmd window and do ctrl+c.**</p>

<br />
<h3>Network Security Groups and Rules</h3>
<p><img src="https://i.imgur.com/dgq0q0I.png" height="80%" width="80%"></p>
<p> We are now going to going to experiment with Network Security Groups within Azure. We are going to implement an inbound security rule which will block ICMP traffic. Navigate to the Azure search bar and type "Network Security Groups". Once you open that menu, click on (Name of your Ubuntu VM)-nsg -> Inbound Rules -> Add. When the side menu opens up, select ICMP as the protocol, Deny as the Type, Priority to some value less than 300, and give it a descriptive name. The goal of this rule is to block ping from reaching the Ubuntu VM. Setting the priority to less than 300 will make it the first rule to be processed by the VM since the next lowest is the SSH rule(Picture as reference).</p>

<p>
  <img src="https://i.imgur.com/47Z60ee.png" height="80%" width="80%">
</p>
<p>Click add and the rule should start taking effect. It may take a bit of time for the rule to go through, but when it does, you will see the perpetual ping we set up earlier show "request timed out" in the terminal. In Wireshark, you should see traffic where it is only the Windows VM requesting ICMP traffic to the Ubuntu VM with "no response found!" at the end of the line.</p>
 <p><img src="https://i.imgur.com/K9j9Qvn.png" height="70%" width="70%"></p>
 <p>If you would like to allow ping traffic again, you'll need to delete the rule. Simply, navigate back to Network Security Groups -> (Your Ubuntu VM name)-nsg > Inbound Rules and click the trash can button shown in the related image.</p>

<br />
<h3>Analyze SSH traffic</h3>
<p><img src="https://i.imgur.com/d5kPpvC.png" height="80%" width="80%"></p>
<p>We will now analyze Secure Shell(SSH) traffic. SSH is protocol that allows for secure remote acess to a device's command line interface on a network. Traditionally this is used to connect to Linux using devices as it is supported natively. However, with external tools you can setup an ssh server on a Windows machine to allow for ssh connection. For this project, we will stick to the Ubuntu VM we've created. If you haven't already, clear the icmp filter from the bar in Wireshark and type either ssh or tcp.port == 22. The second option is the port number and protocol for ssh and isgood to know if you are looking to get into a career in IT. Once Wireshark is set to filter for SSH traffic, establish an SSH connection between the Windows and Ubuntu VM by typing "ssh (username for your Ubuntu VM)@(Ubuntu VM Private IP address)" in the command line and press enter. If you're asked to continue, type yes and enter the password for Ubuntu VM.</p>
<br />
<p><img src="https://i.imgur.com/uRPbJWK.png" height="80%" width="80%"</p>
<p>If the connection is successful, you should see a new console appear with a new line along the lines of "(Your Ubuntu username)@UbuntuClient~:". To create SSH traffic, you will need to type commands in the terminal. The picture above gives some suggestions for what commands to use however there are plenty more to use which can be found online. Here is an explanation of the ones used for this project:
</p>
<ul>
  <li>ls -> lists directories where the user currently is</li>
  <li>pwd -> "Print Working Directory" displays the directory path of the current location</li>
  <li>mkdir -> Creates a new directory at a given location</li>
  <li>whoami -> Displays the name of the current user</li>
  <li>cd -> Changes directory to given one</li>
  <li>touch -> Creates a file at the given location</li>
  <li>nano -> In built Linux text editor</li>
</ul>
<p>The more commands you enter into the terminal, the more traffic can be seen in the Wireshark capture. Notice how you only see new traffic when you enter input into the terminal. It is not a constant stream of information. Once you are done experimenting, you can end the ssh connection by typing exit.</p>
<br />

<h3>Analyze DHCP traffic</h3>
<p><img src="https://i.imgur.com/3vdq4fN.png" height="80%" width="80%"></p>
<p>Next, we will be observing Dyniamic Host Configuration Protocol(DHCP) traffic. DHCP is used to dynamically assign IP addresses to devices within a network. This process is typically done by a router or dedicated DHCP server in an enterprise environment. Our Windows VM is currently getting its IP from Azure itself on our vnet. DHCP traffic can be generated when the DHCP server renews the IP address for a device, which is typically done after a certain lease period. We can manually do this by using the command "ipconfig /renew" in command line. This will instantly release and reassign a new ip address for the VM. To capture the DHCP traffic, filter by using dhcp or udp.port == 67 || udp.port == 68 in the filter bar. Notice how in the output, our source (Windows VM) is making a request to the Azure DHCP service and it Ackknowledges back with a new ip. This is why we are filtering with both port 67 and 68 as this represents traffic from the client making the request and the server responding respectively. </p>

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Windows & Linux Virtual Machine
- Remote Desktop into each Virtual Machine
- Install Wireshark 
- Observe Traffic from Different Protocols using Command-Line & Network Security Groups

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To start observing network traffic, we first need to create two virtual machines on Microsoft Azure. To create the Windows VM:
</p>
<p>
  
  1. On the home webpage, type into the search bar "Virtual Machines" and select the icon
  
  2. Select create virtual machine
     
  3. Give the machine a name such as VM1, and then choose Windows 10 Pro as the image
     
  4. Make sure to give the virtual machine enough virtual cpu size, such as 2vcpus so that the VM doesn't run slow
     
  5. Input a username and password
   
  6. Agree to the liscensing and click "Review + Create", then Create 
  
</p>
<p>
To create the Linux VM, repeat the steps above with a few minor changes:
</p>
<p>

  - Make sure the Linux VM is in the same Resource group, region, & virtual network as the Windows VM (under Networking)
  - Instead of selecting the Windows image, select Ubuntu Server 20.04 LTS
  - Under "Administrator Account" select password instead of SSH public key to create a username and password
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

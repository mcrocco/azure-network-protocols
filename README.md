<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



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
Congrats! You have now created two virtual machines on Microsoft Azure. To remotely connect to each, you can search for "Remote Desktop Connection" on Windows, or if you are using MacOS you can download an app called "Microsoft Remote Desktop". From there, it will ask for a public IP address of your VM. To find this, go back to the Virtual Machines page on Azure and you should see both virtual machines, along with their generated public IP address like the image below. 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Once you select connect in Remote Desktop, enter the username and password you created eariler for the Windows VM. Once remoted in, minimize the window and open another instance of Remote Desktop to remote in to the Linux VM. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the Windows VM, launch Microsoft Edge and search "Download Wireshark" and download the Windows Intel Installer version (refer to the image above). You can also copy and paste this link into the VM: https://www.wireshark.org/. Wireshark allows us to view various networking traffic and filter for specific ports. Once installed, launch Wireshark and select Ethernet and Start Capturing Packets (shark icon). 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we can start observe different network protocols between each VM! The first protocol we will observe is ICMP, which is a protocol used to ensure that packets of data are being sent between two addresses. Specifically, we are going to use the command line tool "ping", which utilizes an ICMP Echo Request & Reply. To do this:
</p>
<p>

1. On Wireshark, filter for "ICMP" in the search bar and hit enter
2. Back in the Virtual Machines page, select the Linux VM and scroll down to find it's private IP address
3. In the Windows VM, open Command Line and type "ping <private IP address>" and hit enter

</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You should see that the Windows VM sent 4 Echo ping requests and got 4 Echo replies from the Linux VM. If we wanted to block ICMP protocols from reaching the Linux VM, we can utilize Network Security Groups on Azure, which basically acts as the VM's firewall. To do this:
</p>
<p>

1. Initiate a non-stop ping with "ping <private IP address> -t"
2. Go to Microsoft Azure and search for Network Security Groups
3. Select the Linux VM's NSG, and then select Inbound security rules
4. Select Add, then ICMP and Deny (you can name it whatever you want)
5. Click Add to create the inbound security rule
6. Go back to Wireshark and the command line, it will start to only send Echo requests on Wireshark and saying "Request timed out" on command line
7. Go back to Network Security Groups and delete the inbound rule that was just createed to see the ping work again with Echo replies
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The next protocol we are going to observe is SSH, or secure shell, which is basically Remote Desktop protocol but you can only use the command line/bash. To do this:
</p>
<p>

1. In Wireshark filter for SSH traffic
2. In the command line, type "ssh <usernameLinuxVM>@<private IP address of Linux VM>" and hit enter
3. Enter yes, then enter password created for the Linux VM
4. Once you have logged in to the LInux VM via SSH, you can type various Linux commands such as "pwd" and observe the traffic on Wireshark
5. Type "exit" to exit SSH
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Dynamic Host Configuration Protocol (DHCP) is the next protocol we are going to observe, which is what dynamically/automatically assigns devices a IP address when it connects to a network. To do this:
</p>
<p>

1. Filter Wireshark for DHCP traffic
2. We can issue the Windows VM a new ip address to see DHCP traffic by going to the command line and entering "ipconfig /renew"
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The next networking protocol we are going to observe is Domain Name System or DNS, which maps human readable text to IP addresses. To observe DNS:
</p>
<p>

1. Filter for DNS in Wireshark
2. In the command line, use "nslookup" to see what a website such as google.com's IP address is
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Our final networking protocol we are going to observe is Remote Desktop Protocol (RDP), which is what we used to log into the Windows and Linux VMs. To do this, simply filter for RDP traffic on Wireshark and do anything on the VM, as the protocol is constantly sending data packets between the VM and our physical device's inputs.
</p>
<p>
Congrats! We were able to successfully observe various types of network traffic through virtual machines on Azure!
</p>
<br />

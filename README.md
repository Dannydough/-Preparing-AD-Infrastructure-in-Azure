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

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic


<h2>Actions and Observations</h2>

Deploy a Domain Controller in Azure

1) Create a Resource Group



* Name the resource group: active-directory-rg
<p>
<img src="https://imgur.com/6IlAVtN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

2) Set Up a Virtual Network and Subnet
* Name the virtual network and subnet: active-directory-vnet
<p>
<img src="https://imgur.com/T1uauFU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

3) Provision the Domain Controller Virtual Machine
   
- Operating System: Windows Server 2022
- VM Name: DC-1
- Username: labuser
- Password: Cyberlab123!

* Once you name the virtual machine "dc-1" you would want to make sure the image is "Windows 2022" as seen in the image below.
<p>
<img src="https://imgur.com/xrI2oyz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>


* Try to make sure the vm size has at least 2 vcpus so that it runs fast. 
<p>
<img src="https://imgur.com/UMt2hg1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>


* Input the username & password in the picture using the (username and password) that is given above.
<p>
<img src="https://imgur.com/AZz1Zgd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>


* Make sure the virtual network and subnet is the one you just created aka "active-directory-vnet"
<p>
<img src="https://imgur.com/Kpfq7zS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

* Your virtual machine is now "FINISHED" (Deployment Complete)
<p>
<img src="https://imgur.com/GLdsyiJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Deploy Client-1 in Azure

4) Provision the Client Virtual Machine

- Operating System: Windows 10
- VM Name: Client-1
- Username: labuser
- Password: Cyberlab123!

*  You must change the new virtual machine name to "client" & the os system aka the image which is "windows 10 pro). You will need to repeat the 3rd step aka creating the virtual machine with the same everything including location, username, password, size, image, and etc.

<p>
<img src="https://imgur.com/YY2JKji.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<p>
<img src="https://imgur.com/1qeV9GM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>


   
* The client-1 virtual machine is finished aka "DONE"
<p>
<img src="https://imgur.com/A9vwOVl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

5) Configure Domain Controller's NIC Private IP Address to Static

- Locate the Network Interface (NIC) associated with the Domain Controller VM (DC-1).
<p>
<img src="https://imgur.com/undefined.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Select IP Configurations under the NIC settings.
<p>
<img src="https://imgur.com/L6hrh06.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Click on the Private IP address and change the assignment from Dynamic to Static. Save the configuration to ensure the IP address remains fixed.
<p>
<img src="https://imgur.com/MV9JhT2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

6) Log into the Domain Controller VM and Disable Windows Firewall (For Testing Connectivity)

- Use Remote Desktop (RDP) to connect to the Domain Controller VM.
<p>
<img src="https://imgur.com/Z8mqmdF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Verify that you are on the correct vm which wil be "dc-1". You will be able to see the "Server Manager" as soon as you open the virtual machine as shown in the picture below. Make sure the virtual machine Operating System is "Windows 2022" as shown in the picture below.
 <p>
<img src="https://imgur.com/zKXbu1q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 
 <p>
<img src="https://imgur.com/mDCxZv9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
- Open the Control Panel and go to System and Security > Windows Defender Firewall.
 <p>
<img src="https://imgur.com/Z8mqmdF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
- Select Turn Windows Defender Firewall on or off.
- Disable the firewall for both Private and Public networks.
- Save the settings. (Ensure this is temporary and re-enable the firewall after testing is complete.)

<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Preparing Active Directory Infrastructure in Azure</h1>

 ###

<h2>Description</h2>
In this project, I set up two Virtual Machines (VMs): one running Windows Server, configured as a Domain Controller, and the other running Windows 10, acting as a client that joins the domain. In future projects, I will deploy Active Directory (AD), execute scripts to create domain users, log into these accounts from the client VM, manage user accounts, and update group policies. This setup effectively simulates a real-world IT environment!
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10 Pro</b>

<h2>Project Walk-through:</h2>

**Deploy a Domain Controller in Azure**

1) Create a Resource Group

- Name the resource group: active-directory-rg
<p>
<img src="https://imgur.com/6IlAVtN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

2) Set Up a Virtual Network and Subnet
- Name the virtual network and subnet: active-directory-vnet
<p>
<img src="https://imgur.com/T1uauFU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

3) Provision the Domain Controller Virtual Machine
   
- Operating System: Windows Server 2022
- VM Name: DC-1
- Username: labuser
- Password: Cyberlab123!

- Once you name the virtual machine "dc-1" you would want to make sure the image is "Windows 2022" as seen in the image below.
<p>
<img src="https://imgur.com/xrI2oyz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Try to make sure the vm size is at least 2 vcpus so that it runs fast. 
<p>
<img src="https://imgur.com/UMt2hg1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Input the username & password in the picture using the (username and password) that is given above.
<p>
<img src="https://imgur.com/AZz1Zgd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Make sure the virtual network and subnet is the one you just created aka "active-directory-vnet"
<p>
<img src="https://imgur.com/Kpfq7zS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
- Your virtual machine is now "FINISHED" (Deployment Complete)
<p>
<img src="https://imgur.com/GLdsyiJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
**Deploy Client-1 in Azure**

4) Provision the Client Virtual Machine

- Operating System: Windows 10
- VM Name: Client-1
- Username: labuser
- Password: Cyberlab123!

- You must change the new virtual machine name to "client" & the os system aka the image which is "windows 10 pro". You will need to repeat the 3rd step aka creating the virtual machine with the same everything including location, username, password, size, image, and etc.

<p>
<img src="https://imgur.com/YY2JKji.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<p>
<img src="https://imgur.com/1qeV9GM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- The client-1 virtual machine is finished aka "DONE"
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
- Right click start menu then click on run > then type "fn.msc" > Windows Defender Firewall.
 <p>
<img src="https://imgur.com/c57zA9t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://imgur.com/IahzJid.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
<p>
<img src="https://imgur.com/l4L3EuB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
- Select Turn Windows Defender Firewall Properties.
   <p>
<img src="https://imgur.com/nW9tCkk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
- Make sure you click on "Private Profile"
  <p>
<img src="https://imgur.com/yEu8Nfa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
- Disable the firewall for both Private and Public networks. Save the settings. (Ensure this is temporary and re-enable the firewall after testing is complete.)
 <p>
<img src="https://imgur.com/9qRCXwR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>  
    
7) Access the Network Interface (NIC) Settings of Client-1:

- In the Azure portal, navigate to the Network Interface (NIC) of the Client-1 VM. Open the DNS Servers settings.

 <p>
<img src="https://imgur.com/uYfZlpV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 

8) Set the DNS Server to the Domain Controller's Private IP Address:

-Select Custom for the DNS server configuration. Enter the Private IP Address of the Domain Controller (DC-1). Save the Configuration: Click Save to apply the DNS settings.

 <p>
<img src="https://imgur.com/reY2N7g.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

 <p>
<img src="https://imgur.com/Z7M8fqG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 

9) Test Connectivity Between Client-1 and DC-1

- Access Client-1: & Connect to the Client-1 VM via Remote Desktop (RDP):
  
 <p>
<img src="https://imgur.com/yXBDZ8G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 

10) Ping DC-1’s Private IP Address:

- Open the PowerShell on Client-1 and then execute the following command: ping (private ip address):

 <p>
<img src="https://imgur.com/31PQwOJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 

11) Verify the Results:

- Confirm that the ping returns replies from DC-1’s Private IP address, indicating successful connectivity.
- If the ping fails, check the following:
- Verify the Private IP address of DC-1.
- Ensure the Windows Firewall on DC-1 is disabled (if still in testing).
- Confirm both VMs are within the same Virtual Network or properly connected through network peering.

 <p>
<img src="https://imgur.com/WZfzswU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 
   
12) Run the ipconfig Command:

- Execute the following command to view the network configuration:
- powershell
- Copy code
- ipconfig /all
- Check the DNS Settings:

- Review the output to confirm that the DNS Server is set to DC-1’s Private IP Address.

<p>
<img src="https://imgur.com/jJYI0dI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 

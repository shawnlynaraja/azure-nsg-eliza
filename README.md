# azure-nsg
Observe network traffic using Wireshark and utilize NSGs
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network Traffic to and from Azure VMs with Wireshark and experiment with Network Security Groups

 <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/6hDtQAX.png" height="80%" width="80%" alt="Creating Resources"/>
</p>
<p>
Part 1 Create Resources within Azure

- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
- While creating the VM, select the newly created Resource Group
- While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
- While creating the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher

</p>
<br /><hr>

<p>
<img src="https://i.imgur.com/tJgKDD1.png" height="80%" width="80%" alt="Install Wireshark"/>
</p>
<p>
Part 2 Observe ICMP Traffic

- Use Remote Desktop to connect to the Windows 10 Virtual Machine
- Within Windows 10 Virtual Machine, Download and Install Wireshark
- Open Wireshark
<p>
<img src="https://i.imgur.com/QnEHRdS.png" height="40%" width="40%" alt="Wireshark"/> <img src="https://i.imgur.com/J8k8pYa.png" height="40%" width="40%" alt="Filter for ICMP"/>
</p>

- Click the blue fin to start capturing packets
- Filter for ICMP traffic only
- Observe that no traffic is captured
- Retrieve the private IP address of the Ubuntu VM
<p>
<img src="https://i.imgur.com/nAL8EJN.png" height="80%" width="80%" alt="Ubuntu Wireshark"/> 
</p>

- Within the Remote Desktop connected to the Windows VM, attempt to ping the Private IP of Ubuntu VM
- Observe ICMP activity in Wireshark 

</p>
<br /><hr>

<p>
<img src="https://i.imgur.com/bzUk8Yt.png" height="80%" width="80%" alt="Observe Ping Requests"/>
</p>
<p>
Part 3 Observe Ping Requests and Replies Within WireShark

- From The Windows 10 VM, open command line or PowerShell
- Attempt to ping a public website (such as www.google.com)
  - Observe the traffic in WireShark
<p>
<img src="https://i.imgur.com/c6UJD28.png" height="40%" width="40%" alt="NSG Disable inbound ICMP"/> <img src="https://i.imgur.com/vjzecTC.png" height="40%" width="40%" alt="Observe ICMP TrafficP"/>
</p>  
  
- Initiate a perpetual/non-stop ping from the Windows 10 VM to the Ubuntu VM
- Open the Network Security Group the Ubuntu VM is using
- Disable incoming (inbound) ICMP traffic
- Observe the ICMP traffic in WireShark and the command line Ping activity (Timed Out)

<p>
<img src="https://i.imgur.com/qevYlv6.png" height="40%" width="40%" alt="NSG Re-enable inbound ICMP"/> <img src="https://i.imgur.com/StI7tdw.png" height="40%" width="40%" alt="Observe ICMP TrafficP"/>
</p>  

- Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using img9
- In the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (resumes)
- Stop the ping activity

</p>
<br /><hr>

<p>
<img src="https://i.imgur.com/t7N8wCc.png" height="80%" width="80%" alt="Observe SSH"/>
</p>
<p>
Part 4 Observe SSH Traffic

- In Wireshark, filter for SSH traffic only (Observe no activity in Wireshark)
- From the Windows 10 VM, “SSH into” the Ubuntu Virtual Machine (via its private IP address)
  - Command: ssh Labuser@10.0.0.5 (Use username from VM2 setup, along with the private IP address for VM2
  -When prompted, enter the password that you used during the setup of VM2
- Observe SSH traffic spam in WireShark
- Exit the SSH connection by typing ‘exit’ and pressing "Enter"


</p>
<br /><hr>

<p>
<img src="https://i.imgur.com/rVLuWTm.png" height="80%" width="80%" alt="Observe DHCP Traffic"/>
</p>
<p>
Part 5 Observe DHCP Traffic

- In Wireshark, filter for DHCP traffic only
- From within Windows 10 VM, attempt to issue your VM a new IP address
  -From the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark
</p>
<br /><hr>

<p>
<img src="https://i.imgur.com/3rWkcXa.png" height="80%" width="80%" alt="Observe D Traffic"/>
</p>
<p>
Part 6 Observe DNS Traffic

- In Wireshark, filter for DNS traffic only
- From within the Windows 10 VM command line
- Use nslookup to see what google.com and disney.com’s IP addresses are
- Observe the DNS traffic being shown in WireShark

</p>
<br />

<hr>


<p>
Part 7 Observe RDP Traffic

- In Wireshark, filter for RDP traffic only, using tcp.port == 3389
- Observe the immediate non-stop traffic being shown in WireShark

</p>
<br />

<hr>


<p>
Part 8 Lab Cleanup

- Close your Remote Desktop connection
- Delete the Resource Group(s) created at the beginning of this lab
- Verify Resource Group Deletion
</p>
<br />

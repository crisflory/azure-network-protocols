
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


Part 1: Setting Up Resources

Create a Resource Group.
![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/c8a323e5-5e42-411f-9ba9-15a7bab08bb6)

Create a Windows 10 Virtual Machine (VM).
When creating the VM, choose the Resource Group you created earlier.
![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/5064da15-3ee9-489b-ad3d-513dfda53c1e)

During VM creation, allow it to create a new Virtual Network (Vnet) and Subnet.

Create a Linux (Ubuntu) Virtual Machine.
When creating the Linux VM, select the previously created Resource Group and Virtual Network.
Observe your Virtual Network using Network Watcher.

Part 2: Observing Network Traffic

Part 2.1: ICMP Traffic (Ping)

Use Remote Desktop to connect to your Windows 10 Virtual Machine.
Inside your Windows 10 VM, install Wireshark.
Open Wireshark and filter for ICMP traffic (Ping).
Find the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM.
Observe ping requests and replies in Wireshark.
From the Windows 10 VM, use the command line or PowerShell to ping a public website (e.g., www.google.com) and observe the traffic in Wireshark.
Start a continuous ping from your Windows 10 VM to your Ubuntu VM.
Open the Network Security Group for your Ubuntu VM and disable incoming (inbound) ICMP traffic.
In the Windows 10 VM, observe ICMP traffic in Wireshark and the command line Ping activity.
Re-enable ICMP traffic in the Network Security Group for your Ubuntu VM.
In the Windows 10 VM, observe ICMP traffic in Wireshark and the command line Ping activity (should start working).
Stop the ping activity.
Part 2.2: SSH Traffic

In Wireshark, filter for SSH traffic only.
From your Windows 10 VM, SSH into your Ubuntu Virtual Machine using its private IP address.
Type in your login information (username, password, etc.) in the Linux SSH connection and observe SSH traffic in Wireshark.
Exit the SSH connection by typing 'exit' and pressing Enter.
Part 2.3: DHCP Traffic

In Wireshark, filter for DHCP traffic only.
From your Windows 10 VM, try to get a new IP address from the command line using 'ipconfig /renew.'
Observe the DHCP traffic in Wireshark.
Part 2.4: DNS Traffic

In Wireshark, filter for DNS traffic only.
From your Windows 10 VM's command line, use 'nslookup' to find the IP addresses of google.com and disney.com.
Observe the DNS traffic in Wireshark.
Part 2.5: RDP Traffic (Remote Desktop Protocol)

In Wireshark, filter for RDP traffic only (tcp.port == 3389).
Observe the continuous stream of traffic. This happens because RDP is continuously transmitting data when connected to another computer, rather than just when you perform specific activities.

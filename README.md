
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

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/56ed1260-a2b3-4ad8-90b6-377787a4d0fe)

During VM creation, allow it to create a new Virtual Network (Vnet) and Subnet.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/5f8b8492-25b6-4451-a513-c43a658413dd)


Create a Linux (Ubuntu) Virtual Machine.
When creating the Linux VM, select the previously created Resource Group and Virtual Network.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/6da2e4e5-a4e0-4cd9-9513-814ba3393f60)

Observe your Virtual Network using Network Watcher.



Part 2.1: ICMP Traffic (Ping)

Use Remote Desktop to connect to your Windows 10 Virtual Machine using its Public IP address and username and password created.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/3110b855-4584-4d18-8143-64c60d9ed1fa)

Inside your Windows 10 VM, install Wireshark.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/cd1f49f5-3bdd-41d7-abba-25b3b62fa3c9)

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/22e913aa-1995-4e30-bee9-03ed67a06376)

Open Wireshark and filter for ICMP traffic (Ping).

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/fda5dd53-1319-4886-8ea4-a57afa708e04)

Find the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/bb58648b-0f93-4999-97ae-bbb6d514f609)

Observe ping requests and replies in Wireshark.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/112c8171-cd99-41c6-ae3e-8563ba2b1c52)

From the Windows 10 VM, use the command line or PowerShell to ping a public website (e.g., www.google.com) and observe the traffic in Wireshark.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/db618cb2-6ef5-4354-9295-1865a6049a58)

click restart current capture on Wireshark and start a continuous ping from your Windows 10 VM to your Ubuntu VM.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/c82e4067-ef29-4130-8996-9965cd3e7c23)

Open the Network Security Group for your Ubuntu VM and disable incoming (inbound) ICMP traffic.

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/815b3ee6-43e4-43bd-a394-1f3f39f917db)

In the Windows 10 VM, observe ICMP traffic in Wireshark and the command line Ping activity.


![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/e2f1e5fb-f892-41be-b943-784f57277f8b)

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


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

Step 1: Create Sample File Shares with Varied Permissions

Create sample file shares with different permission settings.

Step 2: Connect and Log into DC-1 and Client-1

Connect and log into DC-1 using your domain admin account (mydomain.com\jane_admin).
Connect and log into Client-1 as a regular user (mydomain<someuser>).

Step 3: Folder Creation on DC-1

On DC-1, create four folders on the C:\ drive: "read-access," "write-access," "no-access," and "accounting."
![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/d50d0c73-6cef-4430-ac65-640494da47d0)


Step 4: Set Permissions for "Domain Users" Group

For the "Domain Users" group, set the following permissions for the respective folders:
"read-access" folder: Permission - "Read"
"write-access" folder: Permission - "Read/Write"
"no-access" folder: Permission - "Read/Write"
(Skip configuring permissions for the "accounting" folder for now)

![image](https://github.com/crisflory/azure-network-protocols/assets/147748310/7ac12c64-7b25-4827-b852-0e04df2cbd60)

Step 5: Attempt to Access File Shares as a Normal User

On Client-1, navigate to the shared folder by entering "\dc-1" in the Run dialog.
Try to access the folders you created earlier. Note which folders you can access and which ones you can create content in, and evaluate whether it makes sense.

Step 6: Create an "ACCOUNTANTS" Security Group and Test Access

Return to DC-1 and, within Active Directory, create a security group named "ACCOUNTANTS."
Configure the following permissions for the "accounting" folder you created earlier:
"accounting" folder: Group - "ACCOUNTANTS," Permission - "Read/Write"
On Client-1, attempt to access the "accountants" folder as <someuser>. It should result in a failure.
Log out of Client-1 as <someuser>.
On DC-1, add <someuser> to the "ACCOUNTANTS" Security Group.
Sign back into Client-1 as <someuser> and attempt to access the "accounting" share at "\DC-1". Check if access is now granted.
These rephrased steps maintain the original instructions while simplifying the language for clarity. If you require any further modifications or clarifications, please let me know.





# Active-Directory-lab

## Objective

The Active Directory lab provides a controlled environment to explore and practice Active Directory configurations without disrupting real-world systems.  The focus is to understand Active Directory concepts like user, administrator, group management, organizational unit (OU) structures, group policies, and domain trust relationships. The lab also encourages users to explore features, troubleshoot issues, networking, DNS integration and to get comfortable with virtual machines like VirtualBox. This lab helps with getting a better understanding of how the environment works in offices or schools.

### Skills Learned

- User and Group Management: create, modify, and manage user accounts and groups, including setting permissions and managing group memberships. 
- Group Policy Configuration: Practice creating and applying Group Policy Objects to enforce security settings, and manage user enviroments. 
- Domain Controller Admin: Setting up, monitoring, and managing domain controllers.
- DNS Integration: Understand how DNS supports Active Directory and learn to configure DNS settings for seamless Active Directory functionality.
- Trust Relationship Management: Explore the establishment and management of trust relationships between Active Directory domains and forests.

### Tools Used

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Script for user [accounts](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa1cxeEdWYTB6YVltSS0xLUc5WG00WUVpSFF2d3xBQ3Jtc0tuVU9MVUtFS3hoblpTVGF0Z0s5bjdZMzdINVRlTWVuNzdTTENCb2x5RjlDOUp6bmFaMC1HekFUQnVzb0xMWEZYTWdiQlpiZVpCWnYxZXFjeTdTTXgxN3ctU1lqUmR4aVNNeFlLTkhrcEplRmNJU2xYbw&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI)
- Windows 10 [Iso](https://www.microsoft.com/en-us/software-download/windows10)
- Windows server [Iso](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

## Step 1: Create a diagram

  ![AD Diagram](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c68608b1-f97f-4b5c-a829-12c5a6ee2ae6)

*Ref 1: Network Diagram of the Active Directory*

1. Download and install VirtualBox
2. Download Windows 10 and Windows Server ISO
3. Create first virtual machine, the domain controller 
4. Give the domain controller two network adapters, one is going to be used to connect to the outside internet and the other is going to be used to connect the VirtualBox to a private network that the clients are going to connect to.
5. Assign IP addressing for the internal network, the external network will automatically get IP addressing from home network.
6. Name the server, install Active Directory, and create the domain.
7. Configure the domain and routing so the clients on the private network can reach the internet through the domain controller.
8. Set up DHCP on the domain controller so the Windows 10 machine can automatically get an IP address.
9. Run a powershell script that will create 1,000 users for the Active Directory.
10. Create another virtual machine called the Client1 and install the Windows 10 on it. This will connect to the private VirtualBox network.
11. Join Client1 to the domain and log into it with one of the domain accounts.



## Step 2: Install Applications and Virtual Machines

* Download [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Download [Windows Server 2022 ISO](https://info.microsoft.com/ww-landing-windows-server-2022.html)
* Download [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10)

  ![DC settings](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/6be32113-0a87-4788-916a-651417667a73)

*Ref 2: Settings for the Domain Controller*

* The DC needs at least 15 GB to actual work.

* Because there are two NICs in the diagram, there needs to be two adapters
![DC settings adapter1](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/a0cbe243-5f38-4c7c-9570-f6acb0248a54)

*Ref 3: The NAT is already attached to the network and is connected to the house internet*

![DC settings adapter2](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/8bc64443-58c3-45b9-8106-2eba3fe4119d)

*Ref 4: The second adapter is dedicated to the internal vmware, so that is why it is attached to the Internal Network*

* Spin up the DC vm and select the Standard Evaluation Desktop Experience option.

  ![microsoft server OS](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/12db9978-c533-494e-bc38-2f900f5d0459)

*Ref 5: The Standard Evaluation Desktop Experience option makes the command line available*

* When everything works, the default admin account should be displayed.

![DC admin](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c645c168-1600-4cb6-bd6b-822e895e7e77)
*Ref 6: If the vm doesn't have enough space, it will crash*

## Step 3: Setting up and Configuring Domain Controller 

* First, head over to the network so the IP addressing can be set up. The one that's on the internet will automatically get an IP address because of DHCP. The internal one will be set up manually.

![AD Diagram nic outline](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/1e8be94e-8a5e-4ce0-b828-7e4ba42db07c)

*Ref 7: the two NICs are outlined, but only the internal one needs to be configured*

*Navigate to the Network Connections tab and change the names of the adapters to Internal and Internet.

![DC router names](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/9328a2ac-50ab-4edd-9269-e2f5fdda9163)
*Ref 8: to see which is which, check the home IP address for each. The one connected to the internet starts with 10.*

* Next, configure the IP addressing for the internal NIC

  ![AD Diagram internal](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/78d5e61d-805c-4440-8394-1f3de175f562)

*Ref 9: All the relevant info is included in the diagram. The default gateway is empty because the domain controller will be the default gateway*

![internal IP](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/0cfcffd6-59f9-4d78-8a9f-ecf3a5204c1c)

*Ref 10: The preferred DNS server will use itself as DNS*


# Active-Directory-lab

## Objective

The Active Directory lab provides a controlled environment to explore and practice Active Directory configurations without disrupting real-world systems.  The focus is to understand Active Directory concepts like user, administrator, group management, organizational unit (OU) structures, group policies, and domain trust relationships. The lab also encourages users to explore features, troubleshoot issues, networking, DNS integration and to get comfortable with virtual machines like VirtualBox. This lab helps users become proficient in managing directory services.

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

## Step 1
- Create a diagram

  ![AD Diagram](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c68608b1-f97f-4b5c-a829-12c5a6ee2ae6)

*Ref 1: Network Diagram of the Active Directory *

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

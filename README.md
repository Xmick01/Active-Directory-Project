# Active-Directory-lab

## Objective

The Active Directory lab provides a controlled environment to explore and practice Active Directory configurations without disrupting real-world systems.  The focus is to understand Active Directory concepts like user, administrator, group management, organizational unit (OU) structures, group policies, and domain trust relationships. The lab also encourages users to explore features, troubleshoot issues, networking, DNS integration and to get comfortable with virtual machines like VirtualBox. This lab helps with getting a better understanding of how the environment works in offices or schools.

### Skills Learned

- **User and Group Management**: Create, modify, and manage user accounts and groups, including setting permissions and managing group memberships. 
- **Group Policy Configuration**: Practice creating and applying Group Policy Objects to enforce security settings, and manage user environments. 
- **Domain Controller Admin**: Setting up, monitoring, and managing domain controllers.
- **DNS Integration**: Understand how DNS supports Active Directory and learn to configure DNS settings for seamless Active Directory functionality.
- **Trust Relationship Management**: Explore the establishment and management of trust relationships between Active Directory domains and forests.

### Tools Used

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Script for user [accounts](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa1cxeEdWYTB6YVltSS0xLUc5WG00WUVpSFF2d3xBQ3Jtc0tuVU9MVUtFS3hoblpTVGF0Z0s5bjdZMzdINVRlTWVuNzdTTENCb2x5RjlDOUp6bmFaMC1HekFUQnVzb0xMWEZYTWdiQlpiZVpCWnYxZXFjeTdTTXgxN3ctU1lqUmR4aVNNeFlLTkhrcEplRmNJU2xYbw&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI)
- Windows 10 [Iso](https://www.microsoft.com/en-us/software-download/windows10)
- Windows server [Iso](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

## Step 1: Create a diagram

  ![AD Diagram](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c68608b1-f97f-4b5c-a829-12c5a6ee2ae6)

*Network Diagram of the Active Directory*

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

*Settings for the Domain Controller*

* The DC needs at least 15 GB to actual work.

* Because there are two NICs in the diagram, there needs to be two adapters
![DC settings adapter1](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/a0cbe243-5f38-4c7c-9570-f6acb0248a54)

*The NAT is already attached to the network and is connected to the house internet*

![DC settings adapter2](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/8bc64443-58c3-45b9-8106-2eba3fe4119d)

*The second adapter is dedicated to the internal vmware, so that is why it is attached to the Internal Network*

* Spin up the DC vm and select the Standard Evaluation Desktop Experience option.

  ![microsoft server OS](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/12db9978-c533-494e-bc38-2f900f5d0459)

*The Standard Evaluation Desktop Experience option makes the command line available*

* When everything works, the default admin account should be displayed.

![DC admin](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c645c168-1600-4cb6-bd6b-822e895e7e77)
*If the vm doesn't have enough space, it will crash*

## Step 3: Setting up and Configuring Domain Controller 

* First, head over to the network so the IP addressing can be set up. The one that's on the internet will automatically get an IP address because of DHCP. The internal one will be set up manually.

![AD Diagram nic outline](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/1e8be94e-8a5e-4ce0-b828-7e4ba42db07c)

*The two NICs are outlined, but only the internal one needs to be configured*

*Navigate to the Network Connections tab and change the names of the adapters to Internal and Internet.

![DC router names](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/9328a2ac-50ab-4edd-9269-e2f5fdda9163)
*Ref 8: to see which is which, check the home IP address for each. The one connected to the internet starts with 10.*

* Next, configure the IP addressing for the internal NIC

  ![AD Diagram internal](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/78d5e61d-805c-4440-8394-1f3de175f562)

*All the relevant info is included in the diagram. The default gateway is empty because the domain controller will be the default gateway*

![internal IP](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/0cfcffd6-59f9-4d78-8a9f-ecf3a5204c1c)

*The preferred DNS server will use itself as DNS*

## Step 3: Install Active Directory Domain Services 


![AD Diagram AD DS](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c28de3e2-4a7b-48bb-ba39-726ea943e739)

*After the AD DS is installed a domain will be created*

* From the Server Manager, select Add Roles and Features

  ![DC add roles](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/9637fdf3-44e2-445c-a1df-757f8da53923)

*The Add Roles and Features tab allows access to the AD DS*

* After choosing Active Directory Domain Services this will pop up

  ![DC AD domain](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c57caf2c-9cb7-469a-a33a-fdaf629c0426)
![DC AD install](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/998ca13e-38c5-492e-9a45-92b555170d2c)

* A post-deployment configuration is needed because the domain wasn't created before installing AD DS.

![DC post-deployment](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/4ce78591-91e0-4c9b-aeaa-c7a0525e1a92)

* Add new forest and then name the domain: mydomain.com.

![DC root domain](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/00c79b70-6743-4ebc-9c8f-9515d18e159d)
*Installing will cause the computer to restart*

* When everything resets, the menu should look different.

![DC maindomain](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/898d187d-471c-4472-8684-1a405c468741)

* After getting signed in, go to the start window and then click on Windows Administrative Tools and then select Active Directory Users and Computers

  ![DC AD tools](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/ec3b1b18-37b8-4eac-9dc0-76972f706998)

* The newly created mydomain should be in there. If it is, then create an organizational unit to put the admin account in

![organizational unit](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/6ea70d11-76a9-4568-9268-43f9dfa3b248)

* Inside the newly created OU called Admins, add user (admin)

![DC add user](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/f806141e-da13-4766-9059-131c4b4476f7)

* After adding the user make sure it is promoted to admin
![DC user admin](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/affde7e0-21e4-4017-a4ce-81e4fe25667a)

* Log out of the domain controller and sign in as admin to make sure the configurations worked.

![DC admin login](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c6008dbb-ddd0-4626-89fc-6977195ad36d)

## Step 3: Install Remote Access Server and Network Access Translation

![AD Diagram Connection](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/135c15c9-c47b-4dd7-8658-71d7917ba124)
* The reason why RAS/NAT needs to be installed is so that the Windows 10 client can be on the private virtual network but still be able to access the internet through the domain controller.

* Navigate to Add Roles and Features on the Server Manager dashboard and check the Remote Access box and continue to installation.
![DC admin remote access](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/7a9de0a6-81d6-44dc-9a89-0d2c6e14315f)

* After that, click on the Tools tab on Server Manager dashboard and open the Routing and Remote Access option. Select the DC(local) and configure the network for NAT. Select the Internet interface in order to connect to the internet.

![DC AD remote access](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/45cb2383-83bd-4874-846a-15fa0494ccfb)

## Step 4: Set up DHCP Server on the Domain Controller 

* This will allow the Windows 10 clients to get an IP address and will allow them to browse the internet while on a private internal network. This setup would be no different from an office or school.

* Repeating the same steps, select DHCP Server from the Server Roles and continue until installation.
![DC admin remote access DHCP](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/91fd8c34-fa27-4ce8-a3df-937218330001)

* After installation, navigate to Tools and select DHCP so the scope can be established.

![DC DHCP scope](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/83b4517b-c569-461e-8051-afc43625a2cb)

* Enter in the IP range

![DC DHCP ip range](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/107dd792-43e9-48db-a273-8e09174385d0)

* When everything is complete and the DHCP server is authorized, the IPV4 status should be green.

![DC DHCP complete](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/123fc782-ade7-4af4-ad2c-3b28dfb3a583)

## Step 5: Generate 1,000 Users

* Download the [script](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa1cxeEdWYTB6YVltSS0xLUc5WG00WUVpSFF2d3xBQ3Jtc0tuVU9MVUtFS3hoblpTVGF0Z0s5bjdZMzdINVRlTWVuNzdTTENCb2x5RjlDOUp6bmFaMC1HekFUQnVzb0xMWEZYTWdiQlpiZVpCWnYxZXFjeTdTTXgxN3ctU1lqUmR4aVNNeFlLTkhrcEplRmNJU2xYbw&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI) and save it to the desktop.
* Inside the zip file is a txt file with 1,000r randomized names (include your own for realism!)
* Navigate to windows start and run the Windows PowerShell ISE as administrator.
* Open the powershell script that's located in the same zip file as the txt file.
![DC powershell ISE](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/359f992e-a78f-44e2-9a2e-7462fd6f0778)

*set the execution policy to unrestricted and then run the script. 

![DC powershell 1000 names](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/21191c21-bd7c-49a0-b6bd-544493ea826c)

* To make sure that this script works, go to the Active Directory Users and Computers and see if users are added

![DC AD add users confirmed ](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/ea183f9b-0427-4029-b003-d948224766b0)

## Step 6: Create Windows 10 Virtual Machine in VirtualBox

* The internal nic will get its IP address from DHCP server 

![AD Diagram last step](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/f53aadd4-eec9-4ec6-a629-d80fa6d0ab40)

* Download the Windows 10 [Iso](https://www.microsoft.com/en-us/software-download/windows10) and create a new vm in Virtualbox
* Select Windows 10 Pro as the OS
![Client1 windows set up](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/5f71b23c-cada-44de-9077-728299a7a3a2)
* After everything is done installing, check to make sure the internet works.
![Client1 internet check](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/e5a52f97-92a7-4e68-80ce-a0936ae2e249)

![Client 1 checking connection to internet via google](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/64cf2a65-1838-4390-a8d3-a343a155ed26)
* Since google.com resolved that means the DNS server is working.

![AD Diagram ping](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/863dc624-089b-4e33-8b85-462f182cd3c9)
*Client1 has connectivity to the default gateway, the domain controller is properly forwarding it to the internet and the ping comes back as an echo reply*

* Ping mydomain.com, which is the domain controller. It should respond.
![Client 1 mydomain ping](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/d909cf93-ff54-40be-9d6e-6c7fbbd237f1)

*Now that connectivity has been established, it's time to join the domain.
![Connecting client to DC](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/6ffc8965-a3cf-465d-bd57-f464933f01fc)

* Switch over to the DC virtual machine and go to the DHCP server. Click on and expand Scope and the address lease will be available.
![Domain address lease](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/883bd29b-10ae-4cb3-a1f5-e0a478f0d507)

* After joining the client computer to the domain, the client computer will automatically be a member of the domain.

![DC computer client 1 last pic](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/247365f4-542f-43ac-a76d-15f3d71759ce)

* Now that the client computer is part of the domain, any user should be able to log into the Windows 10 client machine.

![sign into domain as admin](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/b5e214a2-5416-47bc-9e3c-2ec2e00d235e)

* After logging on, double-check to make sure that there is connection to the internet.

![double-check connection](https://github.com/Xmick01/Active-Directory-lab/assets/130627895/c9a12ae7-5a50-4bcb-a1a4-94fd16915ed8)

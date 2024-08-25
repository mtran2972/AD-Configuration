<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Configuration in Azure</h1>
This lab builds on the previous exercise where I installed Active Directory and set up a domain controller. In this session, I will configure Active Directory by joining a client machine to the domain and creating user accounts


</p>
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop 
- Active Directory Domain Services
- PowerShell



</p>
<br />

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)



</p>
<br />

<h2>Installation Process</h2>
With Active Directory installed on the domain controller virtual machine, the next step involves creating Organizational Units (OUs) and user accounts. Start by opening the Active Directory Users and Computers console. Right-click on the domain you created, such as mtrantest.com, and select "New Organizational Unit" (OU). Two OUs have been established: _EMPLOYEES and _ADMINS. This naming convention is designed to streamline future use of a PowerShell script.
</p>
Within the _ADMINS OU, create a new user account named Jane Doe. To assign administrative privileges, right-click on Jane's user account, select "Properties," navigate to the "Member Of" tab, and click "Add." Add Jane to the Domain Admins security group to grant her administrative rights. For subsequent administrative tasks, I will use Jane's account, logging off from the labuser account and logging in as jane_admin.

![image](https://github.com/user-attachments/assets/a895ca84-9f35-48bb-b1a9-5cd536f105fb)
![image](https://github.com/user-attachments/assets/29d4ec8c-7d1b-4bbb-bd3f-4e6d1f9c82f5)

</p>
</p>
<br />
<br />

To ensure the client can successfully join the domain, configure the DNS settings before initiating the domain join process. The DNS server must point to the private IP address of the domain controller. Access the Azure portal, go to the Networking tab, select Network Interface, and in the DNS servers section, input the private IP address of the domain controller. Save the changes and restart the client virtual machine to confirm that the DNS settings have been applied correctly.
![image](https://github.com/user-attachments/assets/77753c04-ab70-41d7-b2c4-c8f0c25c28d3)

<br />
<br />
To join the client VM to the domain, navigate to the System menu on the client VM, select "Rename this PC (advanced)," and then "Change." Enter the domain name and the required credentials to complete the process. For this lab exercise, use Jane Doe's credentials, ensuring that the login credentials are entered within the domain context. Once completed, the client VM will be added to the domain and should appear under "Computers" in the Active Directory Users and Computers panel on the domain controller.

![image](https://github.com/user-attachments/assets/97c87487-682c-4b5b-a319-71baa6a2d4a1)
![image](https://github.com/user-attachments/assets/b8ee2115-ca4d-4444-912f-6152511bf3b3)
![image](https://github.com/user-attachments/assets/f7c9b625-9efe-4a4f-b71e-0d9ab4535404)

<br />
<br />
To enable Remote Desktop access for non-administrative users on a client computer within the domain, log in as an administrator. Access System Properties, navigate to the Remote Desktop settings, and select the users permitted to remotely access the PC. Grant Remote Desktop access to Domain Users. Once configured, non-administrative users will be able to log in to Client-1. Typically, a Group Policy would be used to implement this change across multiple systems simultaneously; however, Group Policy will not be utilized for this lab.

![image](https://github.com/user-attachments/assets/e7bc8129-33fa-4601-bef5-f8c5dc574f2c)

<br />
<br />
User creation can be done manually or via a script. For this lab, a PowerShell script will be used. Open PowerShell ISE as an administrator on the domain controller and ensure you are logged in with an administrative account. Create a new file in PowerShell ISE, paste the script into the console, execute it, and monitor the account creation process.

![image](https://github.com/user-attachments/assets/1547dfd4-22f9-4051-bb23-1d1f3927aa1e)
![image](https://github.com/user-attachments/assets/f941cfcd-a86a-476e-9a95-3abd89e62274)

<br />
<br />
After creating the users, Client-1 is ready for sign-in using one of the newly created accounts from the PowerShell script. Choose a username and sign in to the client with the appropriate domain context. In this case, it is mtrantest.com\bon.rovej.

![image](https://github.com/user-attachments/assets/bb11cc96-1059-4d74-8193-50f07742b006)

<br />
<br />



<h2>Lessons Learned</h2>
This lab provided valuable hands-on experience with setting up Active Directory, joining clients to a domain, creating users, and assigning the necessary permissions. Although Active Directory involves navigating through multiple menus, the process is manageable. This lab also served as a foundation for me to explore DNS settings and file permissions in greater depth.

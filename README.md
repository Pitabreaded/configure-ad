<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud and Group Policy management(Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory on Azure Virtual Machines and file share<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Setup 2 Virtual Machines on the same Vnet and set one to be the Domain Controller and the other to be the Client
- Step 2: Access the Domain Controller virtually and install Active Directory Domain Services
- Step 3: Create an Admin in Active Directory Users and Computers
- Step 4: Create a a new Orginzational Unit  called  _EMPLOYEES and create a fake employee
- Step 5: Create shared folders on Domain Controller and set permissions

<h2>Deployment and Configuration Steps</h2>
<p>Client-1</p>
<img width="746" height="185" alt="image" src="https://github.com/user-attachments/assets/4d66df29-d8e5-4748-ab27-96bb57aa2371" />
<p>DC-1</p>
<img width="553" height="153" alt="image" src="https://github.com/user-attachments/assets/d5df3bf8-2716-4a66-9ba4-82b145fe8bee" />
<img width="1312" height="652" alt="image" src="https://github.com/user-attachments/assets/792a7e5c-598f-4847-94f4-68465ab6ec52" />



<p>
Create a virtual machine and name it DC-1 and make sure to make the Source Image Publisher Microsoft Windows Server I used 2022 Data Center and create a second virtual machine named Client-1 and ensure they have the same vNet and the Client-1 Source Image Publisher is Windows. Afterwards ensure you add DC-1 private address as a DNS server for client-1
</p>
<br />

<p>
<img width="981" height="697" alt="image" src="https://github.com/user-attachments/assets/a65b6a3e-bf33-4437-b65f-4f8d6a3045d9" />
<img width="980" height="723" alt="image" src="https://github.com/user-attachments/assets/63adebb2-226e-412b-8dcd-46e28716975e" />

</p>
<p>
Use remote desktop protocol to connect to the DC-1 Virtual Machine and inside the Server Manager install Active Directory Domain Services. Also make sure to click the flag in the top right and click set as domain controller and choose a domain name to use.
</p>
<br />

<p>
<img width="941" height="665" alt="image" src="https://github.com/user-attachments/assets/c086ea15-8225-46b5-9d9b-59a8a456c7c5" />
</p>
<img width="937" height="662" alt="image" src="https://github.com/user-attachments/assets/8de4f8cf-a521-4023-a84d-89f59fd59a09" />
<p>
Open Active Directory Users and Computers and create a new Organizational Group called _ADMINS and open the Organizational Group and create a new user and add them as a member of Domain Admins
</p>
<br />



<p>
<img width="957" height="660" alt="image" src="https://github.com/user-attachments/assets/36c55335-d7c0-4b29-99c6-9207ba7517ad" />
</p>
<p>
Make another Organizational Group called _EMPLOYEES and make another user and add them as a member of Domain Users
</p>
<br />

<p>
<img width="1424" height="815" alt="image" src="https://github.com/user-attachments/assets/07a83f36-75a4-4b7a-945f-7a390afa7513" />
</p>
<p>
From file explorer create a new folders on DC-1's C drive and name them read-access, write-access, and no access and give read, write, or no access to the domain users.
</p>
<br />


<p>
From normal user we created
<img width="1409" height="793" alt="image" src="https://github.com/user-attachments/assets/a8477af9-4101-471a-bd28-1c3dc5b1cddb" />
From admin
<img width="1400" height="796" alt="image" src="https://github.com/user-attachments/assets/a1dd024d-aab2-44b8-bdd7-96cada2a08c4" />
</p>
<p>
Connect to the client VM using the domain you created and then backslash in my case mydomain.com\fse.asd and attempt to access the files and observe that you can edit the files in the write access, can only read in the read access and can't open the folder with no access. If you try to log in using the admin then you can access all of them. 
</p>
<br />

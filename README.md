# Implementing Active Directory within Azure VMs #
<p align="center">
<img src="https://i.imgur.com/p3WJmAI.png" alt="osTicket logo"/>
</p>

<h1>Azure Active Directory - Prerequisites and Installation</h1>
This tutorial outlines setting up Azure Directory on a server and one client that can remote in. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Windows 10
- Windows Server
- Remote Desktop
- Internet Information Services (IIS)
- Azure Active Directory

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>High Level Deployment and Configuration Steps</h2>

- STEP 1 - CREATING THE VIRTUAL MACHINES THROUGH AZURE
- STEP 2 - SETTING DC-1 TO A STATIC IP ADDRESS
- STEP 3 - TESTING CONNECTING FROM CLIENT-1 TO DC-1
- STEP 4 - INSTALLING ACTIVE DIRECTORY
- STEP 5 - CREATE ADMIN AND NORMAL USER ACCOUNTS
- STEP 6 - JOIN CLIENT-1 TO DOMAIN
- STEP 7 - SETTING UP REMOTE DESTKOP FOR NON-ADMIN USERS ON CLIENT 1

<h2>Installation</h2>

STEP 1 - CREATING THE VIRTUAL MACHINES THROUGH AZURE
<p>
<br />
This tutorial will use two virtual machines for this lab. The first one will be named “DC-1” which will be the server VM and the other will be named “Client-1”. See EXAMPLE 1A and 1B for designated settings on portal.azure.com. Login credentials were created and recorded for this lab (admin_user).
<p>
EXAMPLE 1A

![image](https://github.com/Kermini/configure-ad/assets/138714889/f225b820-e7a0-4efa-8c44-e854eb4a9247)


<p>
The next web page several items are input as shown in EXAMPLE 1B & 1C such as Resource Group, Virtual Machine, etc. Ensure to have the inputs be the same as the example photo.
</p>
EXAMPLE 1B

![image](https://github.com/Kermini/configure-ad/assets/138714889/23ad5462-a099-4966-9dce-80366142269e)

<p>
<br />
STEP 2 - SETTING DC-1 TO A STATIC IP ADDRESS
<br />
We select “DC-1”  and on it’s home screen select “Networking” on the left hand side (EXAMPLE 2A).
</p>
<br />
EXAMPLE 2A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/137c652d-91c3-497e-821b-04636e6c4afb)

</p>
<p>
<br />
Once in the networking tab, we select “dc-1703” located to the right of Network Interface, see Example 2B.
</p>
<br />
EXAMPLE 2B
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/27e4ec4b-71ad-442d-95b8-18239549967e)

</p>
<p>
<br />
Then select “IP configurations” shown in EXAMPLE 2C.
</p>
<br />
EXAMPLE 2C
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/a97c1cf5-e257-4adc-b8cd-5a79e1c7c8fd)

</p>
<p>
<br />
Then select “ipconfig1” (towards the bottom) which will lead to screen shown in EXAMPLE 2D. Here we select “Static” and we see that the private IP is “10.0.04” (this is the private IP for DC-1).
</p>
<br />
EXAMPLE 2D
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/ea5535f1-ea35-42ae-96dd-ddcbfdf25572)

</p>
<p>
<br />
STEP 3 - TESTING CONNECTING FROM CLIENT-1 TO DC-1
</p>
<br />
Logging remotely into DC-1 we will enable ICMPv4 traffic to be allowed in order to ping this DC-1 VM from Client-1 VM.
</p>
<br />
EXAMPLE 3A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/3ece7257-fb56-425f-a877-7289d0a38947)

</p>
<p>
We can successfully ping from Client-1 to DC-1 from EXAMPLE 3B.
</p>
<br />
EXAMPLE 3B
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/a10219ec-08c8-4e6e-8ae5-8f441a376a31)

</p>
<p>
<br />
STEP 4 - INSTALLING ACTIVE DIRECTORY
</p>
<p>
<br />
On DC-1 we install Active Directory by first going to the Server Manager and selecting Dashboard and then “Add roles and features” as shown in EXAMPLE 4A.
</p>
<br />
EXAMPLE 4A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/6cbdf40d-8361-4720-9425-b61b4f55c602)

</p>
<p>
<br />
Select “Active Directory Domain Services” when getting to Server Roles as seen in EXAMPLE 4B. Go through the installation steps without additional configurations.
</p>
<p>
<br />
EXAMPLE 4B
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/49b44483-a5b4-41ef-8905-a6f4ea3e1788)

</p>
<p>
When it is completed at the top right of the Server Manager window a yellow sign will display. We went to select “Promote this server to a domain controller” as show in EXAMPLE 4C.
</p>
<br />
EXAMPLE 4C
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/7c5442df-4314-4053-8437-b96ab324cafa)

</p>
<p>
On the first page we will select “Add a new forest” and name the domain name as “Michael.com” for this exercise.  
</p>
<br />
EXAMPLE 4D
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/f15a160e-85f4-4af6-986f-14e765a0faaf)

</p>
<p>
After this installs the DC-1 VM will restart and we will remote back in after it restarts. When we login we will use Michael.com\admin_user now that DC-1 is now a domain controller (EXAMPLE 4D).
</p>
<br />
EXAMPLE 4E
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/36500b33-077c-4078-9cfe-42dc57cdd399)

</p>
<p>
<br />
STEP 5 - CREATE ADMIN AND NORMAL USER ACCOUNTS
</p>
<p>
<br />
Opening “Active Directory Users and Computers” we can begin to add accounts to the new directory that has been created. We will create two new folders named “_EMPOYEES” and “_ADMINS” shown in EXAMPLE 5A.
</p>
<p>
<br />
EXAMPLE 5A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/3e6768d0-5c32-408f-86eb-45d92b70ae9b)

</p>
<p>
We will create a new user named “Matt Hershey” who will be an admin. Right clicking on “_ADMINS” folder we will select “New” and “User” for this.  
</p>
<br />
EXAMPLE 5B
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/77d66b68-74f5-481e-9b54-01357fae1466)

</p>
<p>
On the next page we create a password and unselect “User must change password at next logon” and select “Password never expires”. This is only for the purposes of this tutorial. When this is completed we we still need to give Matt Hershey admin authorization. The folder “Admin” is just a folder with a name at this point. 
</p>
<br />
We will select the folder “_ADMINS” then right click on Matt Hershey and select properties. Then we can select “Member Of” then select “Add…” We can type in domain and check names. Several items will populate and then select “Domain Admins” group. 
</p>
<br />
EXAMPLE 5C
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/090945c0-18a8-4144-9c0a-7df4cfd9a5dd)

</p>
<p>
Now we will log out from the original account of admin_user then log in as an actual admin using Matt Hershey’s account (matt_admin). We will use the username “Michael.com\matt_admin”.
</p>
<br />
STEP 6 - JOIN CLIENT-1 TO DOMAIN
</p>
<br />
We need to set Client-1 DNS settings to the DC-1’s private IP address. Logging into Client-1 we can right click on the widows icon (bottom left) and select settings. On the window we select “Rename this PC (advanced)” as seen in EXAMPLE 6A.
</p>
<br />
EXAMPLE 6A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/ecc19c82-cef8-4d17-a048-f8e550c757ea)

</p>
<p>
Select “Change” box, on the new window select “Domain” and I’ll enter “Michael.com” and select “OK” as shown in EXAMPLE 6B. An error will show up that it could not connect to the domain. This is because it is using a public DNS, we will fix this issue.
</p>
<br />
EXAMPLE 6B
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/b5b9662a-e8e3-453b-a268-4635a232b2da)

</p>
<p>
Going into the Azure Portal we will edit the DNS settings there on the Client-1 VM. We will go to the DNS servers page. These steps include going to Azure Portal > Client-1 VM > Networking > Network Interace: client-1968 (blue link) > DNS Servers (left side). These steps are similar to what we did in Step 2. 
</p>
<br />
Here we can edit the DNS server to be customized to the private IP Address of DC-1, see EXAMPLE 6C.
</p>
<br />
EXAMPLE 6C
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/478d7fce-5d80-4cdf-a04a-fb7845ce877f)

</p>
<p>
We will then restart Client-1, then login using admin_user since it is not connected to the domain yet. We will repeat the steps in EXAMPLE 6A and EXAMPLE 6B to return to the Computer Name/Domain Change window. We will then see a login window in EXAMPLE 6D instead of an error message like before now that the DNS has been set to the domain. We will then login with the admin account that we created on the server and us the domain name as show in EXAMPLE 6D.
</p>
<br />
EXAMPLE 6D
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/c9c21ad7-e8e1-489f-91ab-e8aa53fe31aa)

</p>
<p>

</p>
<br />
EXAMPLE 6E
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/f1a988ba-0ea0-4f0d-be5f-ab3f61ed7063)

</p>
<p>
The Client-1 VM will then need to restart after this configuration. 
</p>
<br />
STEP 7 - SETTING UP REMOTE DESTKOP FOR NON-ADMIN USERS ON CLIENT 1
</p>
<br />
We will then log back in and open settings on Client-1, select “Remote Desktop” then “Select users that can remotely access this PC”. Here we will add the group “Domain Users” so that any of the users can log into this computer. When this is completed it will look like EXAMPLE 7A.
</p>
<br />
EXAMPLE 7A
<p>

  ![image](https://github.com/Kermini/configure-ad/assets/138714889/de4fed44-aea8-4b60-8743-6656fca5e711)

</p>
<p>
END OF TUTORIAL 
</p>
<br />

</p>
<p>

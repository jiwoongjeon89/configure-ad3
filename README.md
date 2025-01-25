<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)
<p>
  Part 3: Exploring Active Directory - Creating Users, Group Policy and Managing Accounts
</p></h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Setup Remote Desktop for non-administrative users on Client-1
- Step 2: Create additional users and attempt to log into Client-1 with one of the users
- Step 3: Group Policy and Managing Accounts 
  
<h2>Deployment and Configuration Steps</h2>

<h3>Setting Up Remote Desktop for non-administrative users on Client-1</h3>
<p>
  We are going to let “normal users” be able to log in to Client-1 via Remote Desktop.
</p>
<p>
<img width="1173" alt="1" src="https://github.com/user-attachments/assets/6391c7e3-2b37-4e78-b147-6d5e502ccce3" />

</p>
<p>
First, we are going to log in to Client-1 as Jane Doe who is an admin with Windows App. 
</p>
<br />

<p>
<img width="1196" alt="2" src="https://github.com/user-attachments/assets/f67de3a9-42ca-4586-9f15-1574bb535ab5" />

</p>
<p>
In the Windows VM, right click Windows button > System > Remote Desktop (under related settings on the right). 
</p>
<br />

<p>
<img width="1197" alt="3" src="https://github.com/user-attachments/assets/ed9ba550-cbcb-4814-99fb-38e3abf6b6a4" />

</p>
<p>
Now click ‘Select users that can remotely access this PC’ > Add > Type ‘Domain Users’ in the box and click OK. 
</p>
<p>
  This has allowed all domain users to be able to log in to Client-1 and after we create users in the next steps, we will be able to demonstrate that.  
</p>
<br />

<h3>Creating additional users and attempting to log into Client-1 with one of the users </h3>

<p>
<img width="1165" alt="4" src="https://github.com/user-attachments/assets/9f427af1-e416-4ff4-a734-adca421b62d7" />
</p>
<p>
Log in to DC-1 as Jane Doe. 
</p>
<br />

<p>
<img width="858" alt="5" src="https://github.com/user-attachments/assets/76d4e77f-ea7d-4eaa-a051-bc56b23e8c2b" />

</p>
<p>
Open PowerShell_ISE as an Administrator by right clicking it. 
</p>
<br />

<p>
<img width="346" alt="6" src="https://github.com/user-attachments/assets/00e9c1a6-7d7a-464f-9a99-0ce168fa98e9" />
</p>
<p>
Create a new file by clicking on this button on the top left. 
</p>
<br />

<p>
<img width="1460" alt="7" src="https://github.com/user-attachments/assets/b7b7853b-ad59-48b7-8d93-e6c446b8e8b9" />

</p>
<p>
Copy this code which will create 1000 users in the _EMPOLYEES folder that we made earlier in the Active Directory Users and Computers (Also, make sure to save the PowerShell file after pasting in the code). 
</p>
<br />

<p>
<img width="1458" alt="8" src="https://github.com/user-attachments/assets/51370c13-61c7-478b-ac4e-38bb7bf04c97" />
</p>
<p>
When you run the code by clicking on the green triangle on the top (or by pressing F5), you will see that it is creating Users with random names.  
</p>
<br />

<p>
<img width="924" alt="9" src="https://github.com/user-attachments/assets/13948920-e061-4f15-8fc2-b0c59bda448b" />
</p>
<p>
Now, when you open Active Directory Users and Computers and go to mydomain.com > _EMPLOYEES, you will see the Users that we created.  
</p>
<br />

<p>
<img width="678" alt="10" src="https://github.com/user-attachments/assets/342a07b3-ffc5-4b79-94fd-ae0546a08d87" />

</p>
<p>
As mentioned earlier, we will now log into Client-1 with one of the users that we have created. 
</p>
<br />

<p>
  <img width="1166" alt="11" src="https://github.com/user-attachments/assets/c3952117-cd2d-416f-8d62-b68ff9bf24fe" />
</p>
<p>
  I have chosen ‘bif.mid’ so the username will be ‘mydomain.com\bif.mid’ and the password will be ‘Password1’  
</p>
<br />

<p>
<img width="1123" alt="12" src="https://github.com/user-attachments/assets/55fb1c91-7c75-4ce3-bfa0-e154a17d163e" />

</p>
<p>
When you are logged in, go to File Explorer > This PC > Windows (C:) > Users and you will see that ‘bif.mid’ has its own profile folder.
</p>
<br />

<h3>Group Policy and Managing Accounts</h3>
<h4>Dealing with Account Lockouts</h4>
One of real-life examples using Active Directory is dealing with Account Lockouts. Using Active Directory, we can set the specifics on the lockout policy.  
<p>

<img width="474" alt="13" src="https://github.com/user-attachments/assets/99ab5402-83f0-4177-80c6-e81420104f40" />

</p>
<p>
To configure the lockout policy, first, log into DC-1 as Jane Doe the Admin > Rick Click Windows button > Run > Type ‘gpmc.msc’ 
</p>
<br />

<p>
  <img width="1193" alt="14" src="https://github.com/user-attachments/assets/b4946f4a-03dc-402b-ba8d-cc87ec658636" />
</p>
<p>
  This will open the Group Policy Management window.  
</p>
<br />

<p>
<img width="1193" alt="15" src="https://github.com/user-attachments/assets/37b19f60-e694-48ae-8beb-fb04ed54bd21" />
</p>
<p>
  Under Forest: mydomain.com > Domains > mydomain.com, you will be able to find the Default Domain Policy. Right click on it and click Edit.  
</p>
<br />

<p>
<img width="1065" alt="16" src="https://github.com/user-attachments/assets/417f8100-9d1a-455a-91a5-253bbc57f404" />

</p>
<p>
 From this window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy. 
</p>
<br />

<p>
<img width="1064" alt="17" src="https://github.com/user-attachments/assets/e5917794-39e8-4fb7-85cd-e9873b0b6fa4" />
</p>
<p>
 In here, you can modify the Account Lockout Duration (The time in minutes that an account remains locked before it is automatically unlocked), 
</p>
<p>
  Account Lockout Threshold (The number of failed logon attempts that will trigger an account lockout), and
</p>
<p>
   Reset Account Lockout Counter After (The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts) 
</p>
<p>
 With those settings, I have now configured the lockout policy for all the Users. 
</p>
<br />

<p>
  Now, I will intentionally fail to log in 5 times as the User ‘bif.mid’
</p>

<p>
<img width="1166" alt="18" src="https://github.com/user-attachments/assets/33e89e97-fc72-469b-9496-86ab9eb54f9e" />

</p>
<p>
  After 5 attempts, I got this message, so the lockout policy is working properly.  
</p>
<br />

<p>

</p><img width="1108" alt="19" src="https://github.com/user-attachments/assets/c055d04a-c458-4e3f-aa78-d618912a1004" />

<p>
 So, when we go to the domain controller (DC-1) and check bif.mid’s account in the _EMPLOYEES folder, you can see that it is locked because there is a check box to unlock the account. 
</p>
<p>
  Checking the box will unlock the account. Also, this is where you can configure many different account settings as the admin.  
</p>
<br />

<p>
<img width="1158" alt="20" src="https://github.com/user-attachments/assets/9cb090c1-3fa8-48e2-9c38-cc363592152e" />
</p>
<p>
 Now that the account is unlocked, I don’t get the message anymore and can log in properly.  
</p>
<br />

<h4>Reseting a User's Password</h4>
<p>
  Another real-life example related to account passwords is resetting a user’s password.
</p>
<p>
  <img width="1107" alt="21" src="https://github.com/user-attachments/assets/e4070d58-11b1-40eb-8c8f-d94ac90cb4ab" />

</p>
<p>
  To do this you can simply right click on any user and click ‘Reset Password’.  
</p>
<br />

<p>
<img width="1109" alt="22" src="https://github.com/user-attachments/assets/43b52c8f-5f85-4486-a9e9-7f491244313f" />

</p>
<p>
  Then, you can set a new password and make the user change it after they log in.
</p>
<br />

<h4>Enableing and Disabling Accounts</h4>
<p>
  Another real-life example using Active Directory is enabling and disabling accounts. 
</p>
<p>
  <img width="1107" alt="23" src="https://github.com/user-attachments/assets/750b3b33-7a06-460a-a663-361f6a3fd8a4" />

</p>
<p>
  Similar to resetting passwords, right click on a user and click ‘Disable Account’.  
</p>
<br />

<p>
<img width="1108" alt="24" src="https://github.com/user-attachments/assets/3debe5dd-7921-4c3a-b4a7-a00e3aa885ee" />
<img width="177" alt="25" src="https://github.com/user-attachments/assets/e48bd288-56e1-45b4-b0f0-e4bdf5a26463" />

</p>
<p>
  You will get this message that the account was disabled, and you can also see that there is a little down arrow next to the User’s icon. 
</p>
 <br />
 
 <p>
<img width="1164" alt="26" src="https://github.com/user-attachments/assets/ac4e9f35-7800-4bb2-9bd0-fdbf14bdc31d" />
</p>
<p>
  Now, if you try to log in as the disabled account, you will see this message that the account was disabled.  
</p>
<br />

<p>
<img width="1111" alt="27" src="https://github.com/user-attachments/assets/30571667-35b3-457b-98e9-56d0cc2938a4" />
</p>
<p>
  Reenabling requires the same steps by clicking the ‘Enable Account’.  
</p>
<br />

<h4>Observing logs</h4>
<p>
  A different kind of real-life example using Active Directory is observing logs. 
</p>
<p>
  This is related to Cybersecurity because logs exist to keep track of every event that happens in a computer system.  
</p>
<br />

<p>
<img width="1280" alt="28" src="https://github.com/user-attachments/assets/203ea0f0-c602-4509-b1bf-1e6e77f9813e" />

</p>
<p>
To check the logs, go to DC-1 and open Event Viewer through the search bar. 
</p>
<br />

<p>
  <img width="2560" alt="29" src="https://github.com/user-attachments/assets/88fb6a24-b279-48ed-a8ae-81ec8ac45626" />
</p>
<p>
  Then go to Window Logs > Security. You can see all the logs which shows everything I have been doing on the DC-1 VM.  
</p>
<br />

<p>
 <img width="505" alt="30" src="https://github.com/user-attachments/assets/d3f05770-97cc-470f-bbf8-89696754027d" />
</p>
<p>
  To find specific logs, rick click on Security and click ‘Find...’  
</p>
<br />

<p>
 <img width="505" alt="30" src="https://github.com/user-attachments/assets/d3f05770-97cc-470f-bbf8-89696754027d" />
</p>
<p>
  To find specific logs, rick click on Security and click ‘Find...’  
</p>
<br />

<p>
  When we look for logs of bif.mid, we can see the events of bif.mid from logging in and out to failure of login, getting locked out, and even Jane disabling bif.mid.  
</p>
<p>
<img width="669" alt="34" src="https://github.com/user-attachments/assets/e33aa81c-6d62-43e8-b2b7-c987cb808c59" />
</p>
<p>
  "The computer attempted to validate the credentials for an account."
</p>
<br />

<p>
<img width="590" alt="33" src="https://github.com/user-attachments/assets/f6718823-5f6e-4650-9cad-79d705941d09" />

</p>
<p>
  "A user account was enabled."
</p>
<br />

<p>
<img width="679" alt="35" src="https://github.com/user-attachments/assets/b44faedb-cd1d-454b-a0b4-bda108f7c5f2" />

</p>
<p>
  "A user account was locked out."
</p>
<br />

<p>
  As you can see, logs can provide loads of information about what happened on a computer from 0 to 100. 
</p>
<br />

<p>
  With Part 3: Exploring Active Directory, this lab has come to an end.  
</p>
<p>
  As you can see, Active Directory is very powerful, and I have only covered the smallest amount of it.
</p>
<p>
  So, have fun with it and explore more when you have the time! 
</p>

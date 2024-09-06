<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
<p>Using Oracle VirtualBox and several VMs to simulate an organization's internal network. A VM for Server 2019 is created
and set as a domain controller. The VM is edited to have 2 network adapters, one for internal network activity and one for 
internet activity. Active directory, DHCP, and other utilities are installed on the server to emulate
an internal network. NAT and RAS are active to allow internet routing for PCs on the private network with the domain  
controller as the default gateway for devices on the network. A Powershell script is used to generate users from a list 
with a generic password. With a second VM installed with Windows 10 Pro, users can connect to the domain with their PC with
their personal credentials.
</p>
<br />


<h2>Programs and Utilities</h2>

- <b>Active Directory</b> 
- <b>Oracle VirtualBox</b>
- <b>PowerShell</b>

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10</b> (21H2)

<h2>Lab Walk Through:</h2>


Create a Virtual Machine for Server 2019 in Oracle VM: <br/><br />
<img src="https://imgur.com/SNT8uoR.png" height="80%" width="80%" alt="Server Creation"/>
<br /> <br />
 

Alter the Network settings: <br/><br />
<img src="https://imgur.com/ny8vmVA.png" height="80%" width="80%" alt="Network Adapter Setting 1"/>
<br /> <br />



Add an Internal Network adapter: <br/> <br />
<img src="https://imgur.com/hn4MdF9.png" height="80%" width="80%" alt="Network Adapter Setting 2"/> 
<br /> <br />





Start the VM and install Server 2019: <br/><br />
<img src="https://imgur.com/WR7ekCT.png" height="80%" width="80%" alt="VM Server installation"/>
 
<br /> <br />


Create the password for the administrator account: <br/> <br />
<img src="https://imgur.com/aKtksPA.png" height="80%" width="80%" alt="Admin account creation"/>
<br /> <br />


Once logged in, view network connections in the control panel. Rename the network adapters to easily identify which is used for Internal network and Internet connections. The internal network adapter should have an unidentified network: <br/> <br />
<img src="https://imgur.com/T6sHuKW.png" height="80%" width="80%" alt="Network adapters"/>
<br /> <br />

Rename the PC in the about page of the system settings, for this example we used DC for domain controller: <br/> <br />
<img src="https://imgur.com/mukbXDn.png" height="80%" width="80%" alt="Rename PC"/>
<br /> <br />

Manually assign an IPv4 address to the DC's internal network adapter. We are using a private address from the range 172.16.x.x:  <br/> <br />
<img src="https://imgur.com/tLdqHr4.png" height="80%" width="80%" alt="Internal network adapter settings"/>
<br /> <br />

The DC will use itself as DNS for the internal network, and will act as the default gateway, 
thus we only need to set the IP address, and use the loopback address for the DNS:  <br/> <br />
<img src="https://imgur.com/7EjUJFW.png" height="80%" width="80%" alt="Internal network DNS"/>
<br /> <br />

Configure the server for active directory. Add roles and features from the server management dashboard. 
Select this PC as the server, identifiable by the new name: <br/> <br />
<img src="https://imgur.com/NGTng0G.png" height="80%" width="80%" alt="Server management AD"/>
<br /> <br />


Continue until the roles page, make sure active directory domain services is enabled and continue.
File and Storage services are selected by default and should be untouched: <br/> <br />
<img src="https://imgur.com/J49GYjy.png" height="80%" width="80%" alt="Select AD"/>
<br /> <br />

Continue through until the installation option appears, and install the server roles. 
Once installed, close the installation window. Open the notification flag and continue with the post-deployment configuration: <br/> <br />
<img src="https://imgur.com/daTPBoe.png" height="80%" width="80%" alt="Complete Installation"/>
<br /> <br />

This server will be promoted to a domain controller. Setup a forest and give a name to this domain.
Set up a password and continue through to complete the deployment configuration: <br/> <br />
<img src="https://imgur.com/4kcBXYQ.png" height="80%" width="80%" alt="Add forest"/>
<br /> <br />
<br/> <br />

<img src="https://imgur.com/HYvWtQv.png" height="80%" width="80%" alt="Domain created"/>
<br /> <br />
<br/> <br />

The VM will restart upon completion of installation. User will be prompted to login with the domain administrator account: <br/> <br />
<img src="https://imgur.com/vyAmgiU.png" height="80%" width="80%" alt="Log in with Admin"/>
<br /> <br />
<br/> <br />

Create a new user in the domain with administrative privileges. Select Windows admin tools under the start menu and click on AD Users and Computers: <br/> <br />
<img src="https://imgur.com/LfR6tLF.png" height="80%" width="80%" alt="AD Users and Groups"/>
<br /> <br />
<br/> <br />

Under your domain, create a new organizational group for administrators and create a new user in for the group: <br/> <br />
<img src="https://imgur.com/52WAj2g.png" height="80%" width="80%" alt="Create Account"/>
<br /> <br />
<br/> <br />

Once the account is created edit it’s properties to give it administrative status. 
To it’s member of property, add Domain Admins as a group, apply the settings and this step will be complete: <br/> <br />
<img src="https://imgur.com/jzbkHj0.png" height="80%" width="80%" alt="Edit Member Of"/>
<br /> <br />
<br/> <br />

This account should be ready to use, log out and type in the account name under other users. 
From here we will add roles and features to install RAS, allowing PCs on the private domain to be able to access the internet through the domain controller.
Under roles we will select Remote access for this feature:  <br/> <br />
<img src="https://imgur.com/3RjTCK1.png" height="80%" width="80%" alt="Roles and features"/>
<br /> <br />
<br/> <br />

Continue through the installer and select Routing under the remote access role services:
<br/> <br />
<img src="https://imgur.com/2aE4YT7.png" height="80%" width="80%" alt="Install RAS"/>
<br /> <br />
<br/> <br />

Close the installation window upon completion and go to routing and remote access. Right-click the current DC and select configure and enable. 
This setup wizard should pop up:<br/> <br />
<img src="https://imgur.com/tb6RRqU.png" height="80%" width="80%" alt="Enable RAS"/>
<br /> <br />
<br/> <br />

From here we will enable NAT and then select the network interface that interacts with the internet:
<br/> <br />
<img src="https://imgur.com/eU6CtVY.png"> height="80%" width="80%" alt="Enable NAT"/>
<br /> <br />
<br/> <br />
<br/> <br />
<img src="https://imgur.com/AoFNLzw.png"> height="80%" width="80%" alt="Select interface"/>
<br /> <br />
<br/> <br />

Next we will add DHCP under roles and services, and install with defaults:<br/> <br />
<img src="https://imgur.com/ey4BiVF.png" height="80%" width="80%" alt="DHCP Roles and Services"/>
<br /> <br />
<br/> <br />

Select DHCP from the server management tools, under the domain create a new scope in IPv4:
The scope can be named anything as long as it's identifiable, here the range of IPs was used:<br/> <br />
<img src="https://imgur.com/FCkTSYH.png" height="80%" width="80%" alt="Creating Scope"/>
<br /> <br />
<br/> <br />

Enter an IP range with appropriate subnetting:<br/> <br />
<img src="https://imgur.com/RdE89FJ.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Add the IP address of the domain controller as the default gateway to allow users in the domain to access the internet:<br/> <br />
<img src="https://imgur.com/nhE8pjD.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

The parent domain will be the current domain. The IP address should already be listed. 
Activate the scope and the DHCP set up is completed:<br/> <br />
<img src="https://imgur.com/Iu5LYnC.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Under server manager, select configure this local server. 
From here select IE Enhanced Security Configuration and set to off, this will allow users to browse the internet.
Now we’ll use a powershell script to generate users from a text file with random names (Original script by Josh Madakor)
Run Powershell ISE as administrator. From here open the script and enter a command to change the server’s execution policy:
<br /> <br />
<img src="https://imgur.com/9tN6jNo.png" height="80%" width="80%" alt="Powershell Script"/>
<br /> <br />
<br/> <br />

Make sure the current working directory is the one with the names text file, and run the script:
<br /> <br />
<img src="https://imgur.com/7fScIAH.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Confirm that the users have been created under AD Users and Groups:
<br /> <br />
<img src="https://imgur.com/ofnJbqz.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Create a client PC VM, representing the computer of a worker in the organization:
<br /> <br />
<img src="https://imgur.com/KBq38Lk.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Edit the VM's network adapter settings, attaching the NIC to the organization's internal network:
<br /> <br />
<img src="https://imgur.com/JaWyffp.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Start the VM, install Windows 10 Pro. Once setup is completed and a generic local user is logged in, enter the command line.
Enter the command ipconfig, to check the PC's network settings and confirm it is connected to the domain:
<br /> <br />
<img src="https://imgur.com/ITcG29L.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Enter the rename menu on the PC in system settings, Rename this PC (Advanced):<br /> <br />
<img src="https://imgur.com/dfnlVpT.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />
Click change to rename the PC as well as join the previously created domain. 
If an error occurs and the PC is unable to join, change the network adapter settings. 
The DNS should not be automatically requested, set it to the internal network address of the DC.
Log into using the credentials of one of the previously generated user accounts when requested.
<br /> <br /><br /> <br />

The DC should have a new address under DHCP leases, representing the client PC:
<br /> <br />
<img src="https://imgur.com/YcYDU9Q.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

We will also see the renamed client PC under the computer directory in AD users and computers. 
Once the PC has joined the domain, they can log in with one of the users that were generated with the powershell script:
<br /> <br />
<img src="https://imgur.com/TrPcVDy.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Log into a generated user on the client PC and confirm it is active in the domain:
<br /> <br />
<img src="https://imgur.com/LuYIa2S.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />

Lastly, confirm the client PC is connected to the internal network and has access to the internet:
<br /> <br />
<img src="https://imgur.com/41hyMKL.png" height="80%" width="80%" alt="IP range"/>
<br /> <br />
<br/> <br />















<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

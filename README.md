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

- <b>PowerShell</b> 
- <b>Oracle VirtualBox</b>

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10</b> (21H2)

<h2>Lab Walk Through:</h2>


Create a Virtual Machine for Server 2019 in Oracle VM: <br/>
<img src="https://imgur.com/SNT8uoR.png" height="80%" width="80%" alt="Server Creation"/>
<br /> <br />
 

Alter the Network settings: <br/>
<img src="https://imgur.com/ny8vmVA.png" height="80%" width="80%" alt="Network Adapter Setting 1"/>
<br /> <br />



Add an Internal Network adapter: <br/> 
<img src="https://imgur.com/hn4MdF9.png" height="80%" width="80%" alt="Network Adapter Setting 2"/> 
<br /> <br />





Start the VM and install Server 2019: <br/> 
<img src="https://imgur.com/WR7ekCT.png" height="80%" width="80%" alt="VM Server installation"/>
 
<br /> <br />


Create the password for the administrator account: <br/> 
<img src="https://imgur.com/aKtksPA.png" height="80%" width="80%" alt="Admin account creation"/>
<br /> <br />


Once logged in, view network connections in the control panel. Rename the network adapters to easily identify which is used for Internal network and Internet connections. The internal network adapter should have an unidentified network: <br/> 
<img src="https://imgur.com/T6sHuKW.png" height="80%" width="80%" alt="Admin account creation"/>
<br /> <br />

Rename the PC in the about page of the system settings, for this example we used DC for domain controller: <br/> 
<img src="https://imgur.com/mukbXDn.png" height="80%" width="80%" alt="Admin account creation"/>
<br /> <br />

Now we will assign an IPv4 address to the DC's internal network. We are using the private address range 172.16.x.x  <br/> 
<img src="https://imgur.com/tLdqHr4.png" height="80%" width="80%" alt="Admin account creation"/>
<br /> <br />


 
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

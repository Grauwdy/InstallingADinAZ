<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Installing Active Directory in Azure</h1>
In this lab, I'll walk you through the steps I took to set up Active Directory using Azure. Think of it as the starting point for some cool labs I've got planned ahead. We're working with two Virtual Machines on Azure, hanging out in the same virtual network. For now, our focus is on one VM—it's going to be our hero, installing Active Directory and becoming the domain controller. The other VM? Well, it's gearing up to join the adventure in a future lab as our trusty client. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/dOOE9KD.png" height="80%" width="80%" alt="Installation Steps"/>
</p>
<p>
Before diving into the VMs, it's crucial to lock in the domain controller VM's IP address as static. By default, if both VMs sport dynamic IPs, even on the same vnet, they won't be able to chit-chat. Without this tweak, our client won't be able to cozy up to the domain we're planning to whip up later.

Head over to the Networking tab for the domain controller VM. Click on the Network Interface and peek at the IP configurations tab. Click on the ipcofig, and don't forget to save your changes. This simple step ensures our domain controller boasts a steadfast IP, playing the role of a rock-solid reference point as we get into the nitty-gritty of configurations.
</p>
<br />

<p>
<img src="https://i.imgur.com/hE1XNtg.png" height="80%" width="80%" alt="Installation Steps"/>
<img src="https://i.imgur.com/hlDtnbY.png" height="80%" width="80%" alt="Installation Steps"/>
<img src="https://i.imgur.com/IbIJWiC.png" height="80%" width="80%" alt="Installation Steps"/>
</p>
<p>
After setting the static IP, it is time to log in to the client VM and see if there is connectivity to the domain controller. Using ping -t (domain controller private ip address), will show that the connection is being timed out. On the domain controller VM, we need to enable ICMPv4 on the local Windows Firewall. Within the search bar, type wf.msc to open Windows Defender Firewall. Click on Inbound Rules and enable the Core Networking Diagnostics - ICMP Echo Request rules. Returning to the client VM will show that the ping is now resolving without errors.
</p>
<br />

<p>
<img src="https://i.imgur.com/88hBLx8.png" height="80%" width="80%" alt="Installation Steps"/>
</p>
<p>
It is now time to install Active Directory on the domain controller VM. With Server Manager open, click on Add Roles and Features and click Next. Confirm the private IP address of the domain controller VM. In the Server Roles tab, click on Active Directory Domain Services. Click Add Features, click Next, then Install. Next we have to promote the server into a domain controller. In Server Manager, there is a warning sign in the top right corner under a flag. Click on that flag and click Promote this server to a domain controller. Click on Add a new forest and specify a domain name. In my case, I will use alaingarciadomain.com Specify a password for the domain and click on Next on each screen and Install.
</p>
<br />

<h2>An Important Note </h2>

When logging back in to the domain controller VM through Remote Desktop Connection, it is important to log in with the context of the domain. Type out the domain path and then the name of the user. For example: mydomain.com\labuser. In my case, it is alaingarciadomain.com\labuser1. Now that Active Directory is installed, configurations can be implemented in future labs and the client VM will be able to join the domain that was created.


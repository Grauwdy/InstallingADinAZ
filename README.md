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

Head over to the Networking tab for the domain controller VM. Click on the Network Interface and peek at the IP configurations tab. Click on the ipcofig a side pane should open to make your edit select the static bubble, don't forget to save your changes. This simple step ensures our domain controller boasts a steadfast IP, playing the role of a rock-solid reference point as we get into the nitty-gritty of configurations.
</p>
<br />

<p>
<img src="https://i.imgur.com/hE1XNtg.png" height="80%" width="80%" alt="Installation Steps"/>
<img src="https://i.imgur.com/hlDtnbY.png" height="80%" width="80%" alt="Installation Steps"/>
<img src="https://i.imgur.com/IbIJWiC.png" height="80%" width="80%" alt="Installation Steps"/>
</p>
<p>
After configuring the static IP, it's time to check connectivity from the client VM to the domain controller. Running ping -t with the domain controller's private IP may initially result in timeout errors. To resolve this, on the domain controller VM, enable ICMPv4 in the local Windows Firewall. Use the wf.msc command in the search bar, navigate to Inbound Rules, and activate the Core Networking Diagnostics - ICMP Echo Request rules. Returning to the client VM should now show successful ping responses without errors.
</p>
<br />

<p>
<img src="https://i.imgur.com/88hBLx8.png" height="80%" width="80%" alt="Installation Steps"/>
</p>
<p>
Time to install Active Directory on the domain controller VM. Here's the quick rundown:

Open Server Manager, select "Add Roles and Features," and hit Next.
Confirm the private IP address of the domain controller VM.
Under the Server Roles tab, click on "Active Directory Domain Services." Add Features, click Next, then Install.
Now, let's promote the server to a domain controller:

In Server Manager, spot the warning sign in the top right corner under a flag.
Click on the flag and select "Promote this server to a domain controller."
Opt for "Add a new forest" and specify a domain name. For example, alaingarciadomain.com.
Set a password for the domain, click Next on each screen, and hit Install. That's it!
</p>
<br />

<h2>An Important Note </h2>

When reconnecting to the domain controller VM via Remote Desktop Connection, remember to log in within the context of the domain. Input the domain path followed by the username. For instance: mydomain.com\labuser. In my scenario, it's alaingarciadomain.com\labuser1. With Active Directory in place, you're all set to dive into configurations in upcoming labs, and the client VM can smoothly join the newly created domain.

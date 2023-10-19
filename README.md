# Configuring-DHCP

This project is an attempt to configure DHCP in a Windows Active Directory. I will be doing so in a virtualized environment with virtual machines of Windows Server 2019 and Windows 10 Enterprise.

# Adding DHCP Feature to Server Manager

To begin, we will have to add the DHCP feature into Server Manager on our Windows Server 2019 system. On the front page of Server Manager:

1. Click on `Manage` on the top right-hand corner
2. Select `Add Roles and Features`

![1  Add Roles and Features](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/ba4860ed-1dd5-4c5b-8d81-317ff8761f78)

Doing so opens the `Add Roles and Features Wizard`. Work your way through the wizard while following these steps:

1. **Before You Begin:** Read through this page and click `Next`
2. **Installation Type:** The wizard, by default, should have `Role-based or feature-based installation` selected. Leave that selected and press `Next`
3. **Server Selection:** Select `Select a server from the server pool` and choose the appropriate server from the list. For me, it would be `Server2019.redlotus.local`, which also happens to be the only server in the pool.
4. **Server Roles:** Select `DHCP Server`
5. **Features:** There is no need to select anything on this page. Simply click `Next`
6. **DHCP Server:** Read the text and click `Next`
7. **Confirmation:** Go through the summary of what you have configured and install the DHCP feature

![2  Click Next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/133725c4-a8c7-4d27-96ed-b4ff73e79cf2)
![3  Click next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/0fcc4d46-a71f-491f-a0e5-8dc9e3f151e2)
![4  Select Server and Click Next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/0c8a303f-e268-4f3d-ac66-1eda8c9996ce)
![5  Select DHCP Server](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/22278d9c-b01a-422c-b6e3-7821464a8957)
![8  Installing](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/c51fbab2-1775-4b7b-9df1-60f8e57aefc8)

Once the installation has finished, click on the blue text that says `Complete DHCP configuration` to open up the post-installation configuration wizard.

![9  Click Complete DHCP configuration](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/f364e19c-8c13-4fe2-a5b0-84b1aa187ad0)

In the post-installation configuration wizard, follow the following steps:

1. **Description:** Read and click `Next`
2. **Authorization:** Select `Use the following user's credentials` and in the text box, enter in the the user that you want to authorize the DHCP server. It is recommended that you use an admin's account. In my case, it would be REDLOTUS/Administrator
3. **Summary:** Read through the summary page and close the wizard to complete

![10  Click Next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/65b424a9-096f-4fcc-9648-261d1c7c301d)
![11  Setting Enterprise Permissions](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/76f6c036-4fa5-44f3-ba68-d22d167dda7e)
![12  Summary](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/e29c366b-f4ac-4309-b7c1-c3f3d5ab5c45)

Now that the DHCP server feature has been added to Server Manager, there are two other tasks that needs to be done. First, on the Windows Server 2019 machine, I previously assigned a static IP address, but for this exercise, I want this system to have an IP address assigned from the DHCP server I just set up. Under the `Network and Sharing Center` in Control Panel, open up the system's network adapter properties page, and then open `Internet Protocol Version 4 (TCP/IPv4) Properties`. Under the IP address settings of this page, select `Obtain an IP address automatically`.

![12-13](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/444303a5-7aff-456a-bd12-d3a3e16466e8)

For the Windows 10 Enterprise system(s), ensure that the IP assignment is set to automatic. To check and/or to change that setting: 

1. Open the `Settings` app
2. Click on `Network & Internet`
3. Click on `Ethernet` and click on the network your system is connected to
4. Under IP settings, click on `Edit`
5. Select `Automatic (DHCP)` and click `Save`

![VirtualBoxVM_6dPOVVFR8l](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/af10eff9-6591-4564-a608-b676c2afae44)

The next task at hand concerns with the virtual machine's settings. If you have any of the virtual machines open, close them and open up their settings page. In the settings page, click into the `Network` tab of the virtual machines. In the `Network` tab, change the network adapter to `Internal Network` because it does not have a built-in DHCP server. After, press `OK` to confirm the changes.

![VirtualBox_aGzN59ooRa](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/2ef5bf0b-c9e8-407c-9543-091721f80e51)

# Creating DHCP Scope

With everything set, we can finally define our DHCP scope. A DHCP scope is a contiguous pool or range of IP addresses. The IP addresses in this pool will be assigned to the systems in our network. In our Windows Server 2019 system, we will enter `DHCP` into the search box located on the taskbar, and select the search result that says `DHCP`. This should open up the DHCP app. On the left-most column, we should see our system listed. Click on the arrowhead pointing right to expand it, showing IPv4 and IPv6 subdirectories. We will then right-click on `IPv4` and select `New Scope` to open up the `New Scope Wizard`.

![13  Creating DHCP Scope part 1](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/0cb971f0-9f20-4734-853e-62fff0333e5d)

Use the following steps for the `New Scope Wizard`:

1. **Scope Name:** Enter a name for the scope and a description. In my case, the name I used was `REDLOTUS Main` and the description was `Main DHCP Server`
2. **IP Address Range:** Enter a start and end IP address for the range of IP addresses that will be used in your network. For me, I entered 192.168.0.51 as the starting address and 192.168.0.100 as the ending address. This means that only addresses from and including 
192.168.0.51 to and including 192.168.0.100 are assignable in your network. Additionally, set the length at `24` and subnetmask to `255.255.255.0`
3. **Add Exclusions and Delay:** The addresses that you define here, which should be within the range defined in step 2, will not be assigned to systems by the DHCP server. The delay defines by how many milliseconds the server waits before offering an IP address. The offering here refers to the DORA process of assigning IP addresses (Discover, Offer, Request, Acknowledge). For the purpose of practice in this project, I have decided to add the address, `192.168.0.52` to be excluded
4. **Lease Duration:** This defines how long a system will use the IP address assigned before needing to return the IP address to the pool or to renew the lease. I have set the lease duration to `8 days`
5. **Configure DHCP Options:** Select yes to configure DHCP options
6. **Router (Default Gateway):** When the DHCP assigns addresses, it also passes information regarding the default router and gateway to the system receiving the IP address as well. For now, we left this empty and moved to the next page.
7. **Domain Name and DNS Servers:** Enter in the name of a domain that you want client systems to use for DNS name resolution. For us, we used our `redlotus.local` domain. Next, enter a server name. For us, it was `Server2019`. 
8. **WINS Server:** Nothing needs to be done here. WINS will not be used.
9. **Activate Scope:** Choose to activate the scope immediately, and click `Next` to activate the scope



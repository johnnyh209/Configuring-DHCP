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
7. **Confirmation:** Go through the summary of what you have configured and install the DHCP feature. 

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

![2  Click Next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/133725c4-a8c7-4d27-96ed-b4ff73e79cf2)
![3  Click next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/0fcc4d46-a71f-491f-a0e5-8dc9e3f151e2)
![4  Select Server and Click Next](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/0c8a303f-e268-4f3d-ac66-1eda8c9996ce)
![5  Select DHCP Server](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/22278d9c-b01a-422c-b6e3-7821464a8957)
![8  Installing](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/c51fbab2-1775-4b7b-9df1-60f8e57aefc8)

Once the installation has finished, click on the blue text that says `Complete DHCP configuration` to open up the post-installation configuration wizard.

![9  Click Complete DHCP configuration](https://github.com/johnnyh209/Configuring-DHCP/assets/33064730/f364e19c-8c13-4fe2-a5b0-84b1aa187ad0)

In the post-installation configuration wizard, follow the following steps:

1. **Description:** Read and click `Next`
2. **Authorization:** Select `Use the following user's credentials` and in the text box, enter in the the user that you want to authorize the DHCP server. It is recommended that you use an admin's account. In my case, it would be REDLOTUS/Administrator.

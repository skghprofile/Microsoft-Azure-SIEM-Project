# Chapter 1: Creating the Azure Virtual Machine

1. After creating and logging into my new Microsoft Azure account, the first thing to do for this project is to set up a new **Virtual Machine** to serve as our honeypot.

&nbsp;

2. From Azure's homepage, there are several ways to create a new virtual machine, but in my example, I clicked **Create a resource** under **Azure services** and then clicked the **Create** hyperlink under **Virtual machine**.

![Screenshot of creating new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img1.PNG)

3. Now that I'm in the **Create a virtual machine** menu, a couple of fields need to be filled out or changed. In the first section, called **Basics**, I did a couple of things:
   - The first thing I did was to create a new resource group to easily manage all the different services I would add to this project. I named this new resource group **HoneypotVMLab**.
   - Next, create a unique name for the new virtual machine (HoneypotVM-01) and select the region in which it will be hosted (East US). 
   - I also needed to change the type of image this machine would run on since the default option was an Ubuntu Server and switched it to a Windows 10 image.

![Screenshot of Basics portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img2.PNG)

4. On the next page labeled **Discs**, I set up the Administrator account with the username: **SteveVMAdmin** and a password that couldn't be easily brute-forced (letters, numbers, and special characters). I also checked the **Licensing** box on the same page.

![Screenshot of Discs portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img3.PNG)

5. On the next page labeled **Networking**, firewall rules can be set for the virtual machine. Since this virtual machine acts as a honeypot, I want connections from the outside to find the machine through any means necessary. To aid in this virtual machine's discovery, I created a new firewall rule to open/allow all inbound ports.
***NOTE: DO NOT DO THIS ON A REGULAR MACHINE! OPENING ALL PORTS IS DANGEROUS AND CAN RESULT IN THE MACHINE OR ORGANIZATION BEING COMPROMISED!***
To create the new rule, the **Advanced** radio button must be selected under **NIC network security group** and then click **Create new** under **Configure network security group** in the box below.

![Screenshot of Networking portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img4.PNG)

6. Now, on the **Create network security group** page, a default rule needs to be removed.

![Screenshot of Create network security group portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img5.PNG)

7. After removing the default inbound rule, **+ Add an inbound rule** can be clicked to create the new rule.

![Screenshot of Create network security group portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img6.PNG)

8. On the **Add inbound security rule page** under **Destination port ranges** a wildcard (*) is added so all port ranges are allowed. I also lowered the **Priority** to **100**, gave this new inbound rule the name: **UNSECURE_ANY_IN**, and saved the new rule.

![Screenshot of Create network security group portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img7.PNG)

![Screenshot of Create network security group portion of new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img8.PNG)

9. All other options can be left as default, so the last thing to create this new virtual machine is to click **Review + create** in the bottom left corner and then deploy the new virtual machine.

![Screenshot of Review + create new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img9.PNG)

![Screenshot of Review + create new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img10.PNG)

10. Quick note:
    - I connected to the new virtual machine to ensure it was created correctly but noticed it was too slow as both the CPU and Memory (RAM) were always at 100% through Task Manager when I was connected.
    - The default machine **Size** of **Standard B1s (1 vcpu, 1 Gib memory)** was too little, so I powered down the virtual machine and changed the **Size** of the machine to **Standard B2s (2 vcpu, 4 Gib memory)** and the virtual machine ran without the lag or stutter I was experiencing before. This also solved the issue of the CPU and Memory being at 100% all the time.

![Screenshot of Review + create new VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c1-img11.PNG)

11. I took note of the newly created **Public IP Address** (**20.55.107.156**) since this is the address I will use to log into the virtual machine in Chapter 4.

&nbsp;

## Next Chapter: 
### [Chapter 2: Setting Up Azure Logs Analytics Workspace](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter2_SetupLAW.md)
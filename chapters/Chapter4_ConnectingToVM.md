# Chapter 4: First Look At New Virtual Machine

- Now that the core setup of this project is completed (Virtual Machine, Log Analytics Workspace, and Microsoft Sentinel), I can connect to the virtual machine and change a couple of options within it before heading back to Azure for the rest of this project.

1. To connect to the virtual machine, I first need the public IP address to connect to. This can be found in the **Overview** section of the virtual machine that was created in Chapter 1. The Public IP address for this machine is **20.55.107.156**.

![Screenshot of Honeypot VM with Public IP Address](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img1.PNG)

2. To connect to the IP address, I searched for the **Remote Desktop Connection** program on my home Windows 10 machine and opened it.

![Screenshot of Remote Desktop Connection Program](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img2.PNG)

3. In the **Remote Desktop Connection** program, I entered the IP from before (20.55.107.156) in the Computer field, used the username I created earlier (SteveVMAdmin), and clicked **Connect**.

![Screenshot of Remote Desktop Connection Program](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img3.PNG)

4. Now that I'm in the virtual machine, there is one thing I want to change to make the machine more discoverable for attackers. I already changed the firewall options through Azure, but I also want to turn off the firewall on the endpoint machine. To do this, I opened the **Firewall & network protection** program that can be easily found through Windows search on the bottom left of the desktop.

![Screenshot of Windows Security Program in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img4.PNG)

5. On the **Firewall & network protection** page of the **Windows Security** application, I turned off the firewall for the **Domain network, Private network, and Public network**.
- Again, turning off the firewall is an awful thing to do and can lead to compromise of the machine or the organization that it is connected to.

![Screenshot of Windows Security Program in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img5.PNG)

6. Now that the firewall is turned off for the virtual machine, I decided to open up the **Event Viewer** program to see if anyone has found the virtual machine honeypot and tried logging into it.
- I can see in **Event Viewer** under **Windows Logs** and **Security** subsection on the left that there are different audit failures and successes.
- I am looking for events with the keyword **Audit Failure** and an Event ID of **4625**.

![Screenshot of Event Viewer in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img6.PNG)

7. To make those audit failures more easily seen, I created a filter for the log to only show the audit failures.
- On the right side of the program, I clicked the **Filter Current Log** button to start the creation of the new filter.
- In the **Filter Current Log** window, I entered the Event ID I wanted to filter for (4625) and clicked **OK** to finish the creation of the new filter.

![Screenshot of Screenshot of Event Viewer in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img7.PNG)

8. Now, I can see the filtered results. There are currently 12 events that have happened so far, but in the later chapters, that number will grow exponentially.
- I can also see through these logs which computer the outside connections tried to connect to and which username they tried to use.

![Screenshot of Screenshot of Event Viewer in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img8.PNG)

9. I can also see which IP address the connection request came from and can quickly look up online where that IP address is located geographically.

![Screenshot of Screenshot of Event Viewer in VM](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c4-img9.PNG)

- At this point, the honeypot is fully configured. Outside connections will passively find this machine and try to make connections to it with a variety of computer names, usernames, and passwords in an attempt to gain access to the machine.
- This information will be collected by the **Log Analysis workspace** that was created and visualized through **Microsoft Sentinel** SIEM dashboards and queries that will be set up in the following two chapters.

<img src="https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/AzureVMOverviewWIP.PNG" alt="Project Overview Diagram With IP" width="600">

&nbsp;

## Next Chapter: 
### [Chapter 5: Creating SIEM Dashboard](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter5_CreatingSIEMDashboard.md)
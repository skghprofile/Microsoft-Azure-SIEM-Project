# Chapter 2: Setting Up Azure Logs Analytics Workspace

- This chapter aims to set up **Log Analytics workspaces** so that event logs from the honeypot virtual machine can be used in Azure.
- This is also useful if the logs are deleted on the virtual machine, they will still be available through Azure.
- I will mainly be using these logs to query information that will be used in the later chapters of this project. 

1. The first step to using **Log Analytics workspaces** is to search for it from the main page of the Azure Portal.

![Screenshot of Log Analytics workspaces search](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img1.PNG)

2. Next is to create a new workspace by clicking the **Create** button on the **Log Analytics workspaces** page.

![Screenshot of Log Analytics workspaces overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img2.PNG)

3. On the **Create Log Analytics workspace** page, I only changed the **Resource group** and **Name** fields.
   - I added the new Log Analytics workspace to the **HoneypotVMLab** Resource group.
   - I also changed the name of the new workspace to **LAW-HoneypotVMLab**.

![Screenshot of creating Log Analytics workspaces](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img3.PNG)

4. After changing those two fields I clicked the **Review + Create** button at the bottom left to create the new **Log Analytics workspace**.

![Screenshot of creating Log Analytics workspaces](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img4.PNG)

![Screenshot of successful Log Analytics workspace](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img5.PNG)

5. Now that the Log Analytics workspace is created and deployed, it needs to be configured to know what data to collect and where to send it. I searched for **Azure Security Center** and opened the new page to start this process.

![Screenshot of Azure Security Center search](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img6.PNG)

6. From the **Azure Security Center** I navigated to **Open Defender for Cloud** at the bottom of the page.

![Screenshot of Azure Security Center overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img7.PNG)

7. On the **Microsoft Defender for Cloud | Overview**, navigate to the **Environment settings** tab on the left side of the page.

![Screenshot of Microsoft Defender for Cloud Overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img8.PNG)

8. On the **Environment settings** page, I expanded the results by clicking the arrow and then clicked the **LAW-HoneypotVMLab** as that is the name of the workspace I created earlier.

![Screenshot of Microsoft Defender for Cloud Environment Settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img9.PNG)

9. On the **Defender plans** page, I turned on both **Foundational CSPM** and **Servers** while keeping the SQL servers on machines off since I won't use any SQL Servers for this project. I then clicked **Save** to ensure the changes were saved before moving on to the next step.

![Screenshot of Microsoft Defender for Cloud Environment Defender Plans](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img10.PNG)

10. On the same **Defender plans** page, I clicked the following menu on the left side called **Data Collection** and clicked **All Events** to ensure that All Windows security and AppLocker events will be saved to the **LAW-HoneypotVMLab Log Analytics workspace**. I also made sure to click **Save** so that the changes will be saved.

![Screenshot of Microsoft Defender for Cloud Environment Data Collection](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img11.PNG)

- Now that the **LAW-HoneypotVMLab Log Analytics workspace** is set up to record security events, it needs to know which machine/server to get those events from. In these next steps, I will connect the created Log Analytics workspace to my virtual machine.

11.  Heading back to the main **Log Analytics workspace** page, I clicked the **LAW-HoneypotVMLab** created earlier to connect it to my virtual machine.

![Screenshot of Log Analytics workspaces overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img12.PNG)

12. On the **Overview** page, the **Virtual** machines (depreciated)** option is located on the left side of the page. Clicking that will show the virtual machines created with this Azure account.

![Screenshot of Log Analytics workspaces overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img13.PNG)

13. I can see **HoneypotVM-01** is listed but not connected. Clicking on it will go to the connect page.

![Screenshot of Log Analytics workspaces Virtual Machines Page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img14.PNG)

14. On this page, I just clicked connect (It's grayed out since it's already connected), and waited for it to finish connecting.

![Screenshot of Log Analytics workspaces Virtual Machines Page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c2-img15.PNG)

- That's it for this chapter. I can now collect logs through Azure from my virtual machine honeypot and use them later when I need to query information related to security events.

&nbsp;

## Next Chapter: 
### [Chapter 3: Adding Microsoft Sentinel](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter3_AddingMSSentinel.md)
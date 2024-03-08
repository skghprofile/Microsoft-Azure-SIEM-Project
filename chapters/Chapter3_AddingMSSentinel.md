# Chapter 3: Adding Microsoft Sentinel

- In this chapter, I will set up the **Microsoft Sentinel** service inside Azure so I can visualize events through dashboards and queries in the later chapters.
- **Microsoft Sentinel** will use the log data from the **Low Analytics workspace** I set up in the previous chapter.

1. The first step in adding **Microsoft Sentinel** is to search for the service at the top of the primary Azure page.
   
![Screenshot of Microsoft Sentinel search](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c3-img1.PNG)

2. On the **Microsoft Sentinel** page, I clicked the **Create** button in the top left to select which **Low analytics workspace** to add it to.

![Screenshot of Microsoft Sentinel main page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c3-img2.PNG)

3. On the **Add Microsoft Sentinel to a workspace** page, I clicked my created **LAW-HoneypotVMLab** workspace and clicked **Add** on the bottom left of the page.

![Screenshot of Microsoft Sentinel add to workspace](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c3-img3.PNG)

4. That's all there is to add **Microsoft Sentinel** to my created log analytics workspace. In a later chapter, I will go more in-depth with this service since Microsoft Sentinel is what I'll be using to develop the SIEM dashboard and query information through the logs it has collected.

![Screenshot of Microsoft Sentinel overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c3-img4.PNG)

&nbsp;

## Next Chapter: 
### [Chapter 4: First Look At New Virtual Machine](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter4_ConnectingToVM.md)
# Chapter 5: Creating SIEM Dashboard

- In this chapter, I will create a simple SIEM dashboard that will look like the dashboard in the image below. The dashboard will show how many failed login attempts happened every 30 minutes, the amount of failed logins from the top IP address sources with the most failed connections, and the most popular usernames outside connections attempted to log in with.

![Screenshot of example SIEM dashboard](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img1.PNG)

1. The first step to creating the dashboard is to open up the **Microsoft Sentinel** service.

![Screenshot of Microsoft Sentinel Search](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img2.PNG)

2. Next, click the **LAW-HoneypotVMLab** that was created in chapter 3 of this project.

![Screenshot of Microsoft Sentinel Overview page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img3.PNG)

3. From there, I navigated to the **Workbooks** section on the left side of the page and clicked **+ Add Workbook** to create a new workbook that will serve as the location for the new dashboard

![Screenshot of Microsoft Sentinel Workbooks page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img4.PNG)

4. After creating a new workbook, there will be default visual analytic graphs that need to be removed. The first step to remove them is to edit the workbook by clicking the **Edit** button near the top of the page.

![Screenshot of New workbook page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img5.PNG)

5. Next, I will click the blue **Edit** button at the bottom right of each module and then click the **Remove** button to remove the default analytic graphs.

![Screenshot of New workbook query edit](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img6.PNG)

![Screenshot of New workbook query removal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img7.PNG)

6. Now I have a blank workbook that I can add my graphical queries to. To create a new query, I'll click **Add** and then **Add query**.

![Screenshot of New workbook add](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img8.PNG)

![Screenshot of New workbook add query](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img9.PNG)

7. With the new query created, I want the first visualization for my dashboard to show how many failed login attempts are made every 30 minutes using a bar chart. The first step is to add the KQL query below:

```
SecurityEvent
| where EventID == 4625
| summarize FailedLoginCount = count() by bin(TimeGenerated, 30m)
```
- This query can easily be explained line by line:
  - **SecurityEvent** is the data source. This is where the query will start looking for data.
  - **| where EventID == 4625** filters data from the **SecurityEvent** source is to only show data with an Event ID equal to 4625.
  - **| summarize FailedLoginCount = count() by bin(TimeGenerated, 30m)** summarizes the filtered data under the new name created **FailedLoginCount**. This summarized data is also filtered by count, and the **bin(TimeGenerated, 30m)** groups the events into 30-minute intervals so each bar on the bar chart represents 30 minutes.

- The other settings I changed on this new query page were the **Time Range** to **Last 7 Days** and the **Visualization** to **Bar Chart**.


![Screenshot of New query settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img10.PNG)

8. I navigated to the **Advanced Settings** page at the top of the new query to add a new **Chart title** (Failed Login Count (30m)) to easily show other users who may look at this dashboard what the bar chart represents.

![Screenshot of New query advanced settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img11.PNG)

9. After clicking **Run Query** on the main settings tab, the query is now shown as a bar graph with a title at the top of the chart.
- The last thing I needed to do to complete this first visualized query was to click **Done Editing** in the bottom left of the query editor. 

![Screenshot of New query settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img12.PNG)

10. The subsequent two queries will follow a similar format with only a slight difference or two between them.
- For this following query that shows the most failed connections by the same IP addresses I first created a new query as shown in step 6.
- I then added the query below:

```
SecurityEvent
| where EventID == 4625
| summarize FailedLogins = count() by IpAddress
| sort by FailedLogins desc
```
- As shown, the first two lines of the KQL query are the same but the last two are different.
  - In the **| summarize FailedLogins = count() by IpAddress** line, I want to get the IP Addresses of the attempted connections, so the correct field to do so in KQL is to use **IpAddress**.
  - I also want to sort the count in descending order to see who the prominent actors are, which is accomplished in the **| sort by FailedLogins desc** line of the query.

- After entering in the query I changed the **Time Range** to **Last 7 Days** and the **Visualization** to **Bar Chart** just like the first query made before.

![Screenshot of New query settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img13.PNG)

12.  As with the first query, I navigated to the **Advanced Settings** page at the top to add a new **Chart title** (Failed Login IP Addresses) to easily show other users who may look at this dashboard what the bar chart represents.

![Screenshot of New query advanced settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img14.PNG)

13. There was one last thing I wanted to try with these final two queries: to try and split them side by side so each query took up 50% of the horizontal space. Luckily, this was easy in the **Style** tab of the query. I checked the box **Make this item a custom width** and added the number **50** to the **Percent width** field.
- I also checked the **Show border around content** box to make the separation between queries easier to distinguish from the others.
- With all the changes finished for the **Style** tab, I clicked **Done Editing** at the bottom to complete the query.

![Screenshot of New query style](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img15.PNG)

14.  This last query is shown in a format different from the first two. I wanted to create a pie chart showing the most attempted usernames. As before, this query follows a format similar to the one used to enter the query below.

```
SecurityEvent
| where EventID == 4625
| summarize FailedLogins = count() by Account
| sort by FailedLogins desc
```

- The only difference between this query and the one before is the **Account** instead of **IPAddress** in the third line of the query. This tells the query to pull the Account (username) from the filtered Security Event data source.
- I also changed the **Time Range** to **Last 7 Days** and the **Visualization** to **Pie Chart**.

![Screenshot of New query settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img16.PNG)

15. In the **Advanced Settings** tab I changed the **Chart title** to **Failed Username Count**.

![Screenshot of New query advanced settings](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img17.PNG)

16. As with the previous query, I wanted this query to fill the other half of the horizontal space, which could be accomplished in the **Style** tab.
- In this tab I checked **Make this item a custom width** and entered **50** into the **Percent width** field.
- I also checked the **Show border around content** box to make the separation between queries easier to distinguish from the others.
- With all the changes finished for the **Style** tab I clicked **Done Editing** at the bottom to complete the query.

![Screenshot of New query style](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img18.PNG)

1.  With the three queries adequately set up, it is time to save the workbook.
- The process of saving the workbook starts with clicking the floppy disc icon near the top of the page.

![Screenshot of New workbook overview](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img19.PNG)

18. On the right side of the screen, a new window popped up where I could give the new workbook a **Title** and assign it to the **Resource group** I created at the start of this project in Chapter 1.

![Screenshot of New workbook save as screen](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img20.PNG)

19. After entering the **Title** (Honeypot VM Dashboard) and assigning it to the (HoneypotVMLab) **Resource group**, I clicked apply at the bottom of the **Save As** page to save the changes made.

![Screenshot of New workbook save as screen apply button](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img21.PNG)

20. Heading back to the **Microsoft Sentinel** service under the **Workbooks** tab, I can now see the saved workbook dashboard under the name **Honeypot VM Dashboard**.
-Clicking the name **Honeypot VM Dashboard** and then **View saved workbook** at the bottom right of the page will open it up on a new page.

![Screenshot of updated Microsoft Sentinel Workbooks page](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img22.PNG)

- That's it! Here is the view of the saved worksheet.

![Screenshot of updated Dashboard](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c5-img23.PNG)

- In the next chapter, I want to go into more detail with the logs collected by Microsoft Sentinel by using the **Logs** section and trying a few simple queries.

&nbsp;

## Next Chapter: 
### [Chapter 6: Analyzing Logs in Azure with KQL](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter6_AnalyzingLogs.md)

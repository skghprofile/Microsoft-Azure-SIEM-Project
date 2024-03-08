# Chapter 6: Analyzing Logs in Azure with KQL

- In this chapter, I want to use more queries to inquire about more details from the questions I had when looking at the dashboard and progressing through the project in general.
- My biggest question was if someone could successfully log into the machine and how they did so.
- I also wondered how close they got if no one successfully logged into the machine.
- I also knew that using KQL would be the only way I could find answers to my questions because of the tens of thousands of different events that were logged and using a query would pull the correct information I needed instantly.

1. To start this chapter I navigated to the **Microsoft Sentinel** service and **Logs** on the left side to open the **Queries** screen

![Screenshot of Microsoft Sentinel Logs tab](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img1.png)

2. Since there are many prefilled queries I clicked the **X** in the top right corner of the **Queries** screen as I will be doing my own custom queries.

![Screenshot of Queries screen with X highlighted](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img2.png)

3. With the queries screen ready for input, I entered my first query.
```
SecurityEvent
| where EventID == 4624
| summarize SuccessfulLogin = count() by Account, Computer, IpAddress
| sort by IpAddress desc
```
- I will break down this query which is mostly similar to the query from the SIEM Dashboard in the previous chapter.
  - **SecurityEvent** : is the data source.
  - **| where EventID == 4624**: Filters for **successful login events** on the local computer or in this case the virtual machine honeypot.
  - **| summarize SuccessfulLogin = count() by Account, Computer, IpAddress**: This line creates a new column called **SuccessfulLogin** and counts the occurrences with the **count()** portion of the line. This line also grabs the computer account that was logged in to, the computer that was logged in to, and the source IP address that the login request came from.
  - **| sort by IpAddress desc**: This line sorts the results by the **IPAddress** field in descending  order.

&nbsp;

- The results in the image below show some interesting insights:
  - The **HoneypotVM-01\SteveVMAdmin** results under the **Account** column are successful logins into the virtual machine honeypot. The two lines from this query are from my local machine, one with my personal IP address and one with an IP address from a VPN.
  - This also means that no unknown external connections were successfully made into the virtual machine account with successful credentials.

&nbsp;

- The results also show that there were some successful unknown external connections to the **NT AUTHORITY\ANONYMOUS LOGON** and **WORKGROUP\ANONYMOUS LOGON** accounts.
  - Although these accounts are not tied to specific users or groups, they show concern since the **WORKGROUP** account is used for file sharing and printer access over the network in an unencrypted format.
- Later in this chapter, I will go into more detail about the IP addresses of these external connections.


![Screenshot of query showing successful logins](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img3.png)


4. Since I established that there were no credentialed unknown external logins, I was curious if any external connections came close to finding the correct username for the virtual machine honeypot.
- For this, I started a new query by clicking the *+* at the top of the queries screen to open a new tab.
- With the new query, I entered in:
```
SecurityEvent
| where EventID == 4625
| search "Steve*"
| summarize FailedLogins = count() by Account,Computer, IpAddress
| sort by FailedLogins desc
```
- As with the previous queries, I followed a similar format. I wanted to search for failed logins using the **| where EventID == 4625** and wanted to search for anything related to the username **HoneypotVM-01\SteveVMAdmin** by filtering the search with the line **| search "Steve*"**.
  - This line includes the wildcard **"*"** after **Steve** to filter any results starting with "Steve" and anything after it.
- As shown in the image below, no external connections came close to finding the correct username and instead just sprayed with simple or default usernames.


![Screenshot of failed login query account username "Steve*"](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img4.png)

5. To verify that the above query would find the username **HoneypotVM-01\SteveVMAdmin**, I created another quick query substituting **| where EventID == 4625** with **| where EventID == 4624** for successful logins and found the two connections I made to the machine.

![Screenshot of successful login query account username "Steve*"](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img5.png)

6. Taking a quick sidetrack, after initially setting up the SIEM Dashboard and watching the connections being made, I saw something interesting. There were connection attempts from a single IP address, and they quickly found the machine's name.
- I thought I'd investigate a little further and query their IP address with a new query by entering in:
```
SecurityEvent
| where EventID == 4625
| search  "62.204.41.107"
| summarize FailedLogins = count() by Account,Computer, IpAddress
| sort by FailedLogins desc
```
- I was intrigued by the results. The external connection started out trying to connect with a **\Test** username but then quickly figured out the exact name of my virtual machine honeypot **\HoneypotVM-01**.
- The connection then tried to use **\HoneypotVM-01** and **\HoneypotVM-01\HoneypotVM-01** in hopes that those may be the usernames of the machine.

![Screenshot of failed login query with specific IP address](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img6.PNG)

7. A week later, I wanted to see if this connection made any other interesting discoveries about my honeypot virtual machine.
- I started a new query and entered in:
```
SecurityEvent
| search  "62.204.41.107"
```
- What I saw with the results below was fascinating and shows how these bots/scripts work on a surface level.
- Here is my theory on what is happening:
  - The bot/script uses a sample username of **Administrator** and **Test** to establish a connection to the machine that eventually fails.
  - Even though the connection failed, it learned the name of the machine **HoneypotVM-01**.
  - The bot/script then tries to use the newly acquired computer name to try and log in with **HoneypotVM-01** and **HoneypotVM-01\HoneypotVM-01**, but those eventually fail too.
- What surprised me the most was that these external connections were cyclical, happening every day with the process looking like this: (**Administrator** -> **Test** -> **HoneypotVM-01** -> **HoneypotVM-01\HoneypotVM-01**).

![Screenshot of failed login query with specific IP address](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img7.PNG)

8. The last part of this chapter is revisiting and investigating in further detail the successful connections to the **NT AUTHORITY\ANONYMOUS LOGON** and **WORKGROUP\ANONYMOUS LOGON** accounts as shown in **Step 3** using [VirusTotal URL Search](https://www.virustotal.com/gui/home/search).

&nbsp;

- The connection made to the **NT AUTHORITY\ANONYMOUS LOGON** account was the only one on that list with an IP address that originated from France.

&nbsp;

- All the other connections that logged into the **WORKGROUP\ANONYMOUS LOGON** account were Belarusian IP addresses that are likely malicious and used in bot traffic to execute scripts.
- The **Community** tab with comments from other users that encountered the same IP address helps narrow down that these IP addresses are used to facilitate different types of attacks like:
  - Apache Attacks.
  - Brute Force Attacks
  - FTP Attacks.
  - IOC Attacks using Python requests as a user agent to enumerate sensitive directories.


![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img8.PNG)

![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img9.PNG)

![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img10.PNG)

![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img11.PNG)

![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img12.PNG)

![Screenshot of IP address result from VirusTotal](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img13.PNG)

9. While investigating the IP address that originated from France near the start of this project, I accidentally copied and pasted the address into the browser and was met with an unexpecting web page. I noted that the IP address directly connected to a web page and wanted to document it later with screenshots but was unable to recreate the path to the web page directly with the IP address.
- I used another IP address lookup website and found the hostname associated with the IP address **scan072.intrinsec.com**.

![Screenshot of IP address lookup result](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img14.PNG)

10. Entering the hostname into a browser led me to a webpage with the new URL **abuse.intrinsec.com**, and I was surprised to see the exact text I saw when I first accidentally discovered this webpage.
- From this little investigation into a singular IP address, I learned that along with external connections from malicious traffic on the internet, there is also traffic from legitimate sources that are constantly crawling the internet for non-malicious purposes.

![Screenshot of Intrinsec webpage](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c6-img15.PNG)


- In the next chapter, I'll summarize my findings and conclusions from this project.

&nbsp;

## Next Chapter: 
### [Chapter 7: Findings and Conclusions](https://github.com/skghprofile/Microsoft-Azure-SIEM-Project/blob/main/chapters/Chapter7_FindingsConclusions.md)
#Chapter 7: Findings and Conclusions

###This chapter will go into detail with my findings and conclusions from this project that took place over a total timespan of just over a week (~8 days).

&nbsp;

- Over the 8 days of this project, there were a total of over **314,000+** unsuccessful external connections made to the honeypot virtual machine.
- The top 10 most failed connections to the honeypot virtual machine are as follows:

| IP Address      | # Of Connections | IP Country Source  |
| --------------- | ---------------- | ------------------ |
| 45.141.87.103   | 77.8k            | Russia             |
| 111.12.168.74   | 12.4k            | China              |
| 190.6.140.54    | 11k              | Dominican Republic |
| 109.124.81.93   | 11k              | Russia             |
| 185.216.246.162 | 11k              | Russia             |
| 185.225.233.153 | 9.79k            | Germany            |
| 103.167.114.208 | 6.25k            | Indonesia          |
| 176.111.174.178 | 6.1k             | Russia             |
| 185.161.248.30  | 5.21k            | Russia             |
| 194.26.135.117  | 5.18k            | Russia             |
| All Other IPs   | 135k             | N/A                |

- The top 10 most used failed usernames to the honeypot virtual machine are as follows:

| Username                    | # Of Occurances |
| --------------------------- | --------------- |
| administrator               | 129k            |
| ADMINISTRATOR               | 18k             |
| HONEYPOTVM                  | 12.9k           |
| Administrator               | 11.9k           |
| ADMIN                       | 2.12k           |
| domainname\administrator    | 1.52k           |
| domain\administrator        | 1.51k           |
| HoneypotVM-01\Administrator | 1.26k           |
| HoneypotVM-01\HoneypotVM    | 1.2k            |
| HoneypotVM-01\01            | 1.07k           |
| (All Other Usernames)       | 132k            |

![Screenshot of SIEM dashobard overview at end of project](https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/c7-img1.PNG)

- Along with the **314k+ failed connections** there were **10 successful anonymous connections** and **0 unknown credentialed successful remote connections** to the virtual computer honeypot.

#What I learned

- Initially, I learned how to set up a virtual machine in **Microsoft Azure**, collect logs using **Azure Log Analytics workspaces**, and configure a dashboard within **Azure’s Microsoft Sentinel**. However, what I didn’t anticipate was the wealth of knowledge I’d gain through real traffic analysis and my investigation into the logs collected after the initial setup.
- I thought I learned a lot looking through my cybersecurity textbooks and online videos befire starting this project, seeing security principles in action was an entirely different experience. This project has been an eye-opener, revealing how networks and computers connected to the internet are constantly under attack. Without robust security controls, they become vulnerable targets. 
- I learned that the automated bots/scripts I encountered in this project rely on people who set up systems on the internet with default usernames and simple passwords. I was honestly surprised by the sheer amount of connections that were made with a variation of the username "Administrator" or the computer's name "HoneypotVM-01". This still makes me wonder how often computers and networks still use simple usernames and passwords, since these types of automated attacks are still used in 2024.

&nbsp;

- Through this project I researched more about the **Anonymous Logons** through the default **Workgroup** and **NT Authority** accounts since there were unknown successful connections made through them.
- I learned that even with enabling the **Windows Firewall**, it doesn't restrict anonymous logons to a workgroup. Instead, it has to be disabled through the local machine's Windows Registry or through Group Policy.

#Conclusion

- This project showed and emphasized the importance of serveral aspects related to computer and network security:
  - Vulnerability to External Threats: Connecting computers or networks to the internet without proper security practices in place can lead to easy compromise by external threat actors.
  - Usernames and Passwords: The significance of avoiding default usernames like "Administrator" and emphasizing the use of complex passwords.
  -  Constant Threat Landscape: By merely being connected to the internet, computers and networks can face thousands of attempted connections daily. Knowledgeable network administrators and the use of robust security controls are essential to safeguard against these persistent threats.
  - Firewall Configuration: To mitigate attacks similar to the one encountered in this project, enabling and configuring firewalls becomes crucial. By blocking unnecessary ports and those not in active use, we can significantly enhance security. The primary ports associated with the attacks observed in this project include:
    -  TCP 3389 for Remote desktop connections.
    -  TCP/UDP 445 for file and printer sharing in a workgroup.
    -  TCP/UDP 137 - 139 for NetBIOS services (which might explain how external connections learned the virtual machine honeypot name).
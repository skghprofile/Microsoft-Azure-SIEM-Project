# Microsoft Azure SIEM Honeypot Project 2024

## Project Objectives

- Set up a honeypot on Microsoft Azure.
- Expose the honeypot to the internet.
- Monitor and document RDP connections.
- Analyze the data collected by the honeypot.
- Investigate traffic from specific IP addresses.

## Overview of the Project

 1. Create a **Free Azure Account** (with $200 in free credits for the first month)
 2. Set up a new **Virtual Machine** in Azure to use as the honeypot for the project.
 3. Create a new **Log Analytics Workspace** to aggregate the event logs from the Virtual Machine.
 4. Set up **Azure Sentinel** with Azure. (Microsoft's cloud-native SIEM).
 5. Create a **SIEM dashboard** in **Azure Sentinel** for viewing log data.
 6. Use queries in **Logs** tab of **Log Analytics Workspace** to investigate specific incidents in more detail
 7. Show results and document the importance of security principles.

<img src="https://raw.githubusercontent.com/skghprofile/Microsoft-Azure-SIEM-Project/main/images/AzureVMOverview.PNG" alt="Project Overview Diagram" width="600">

## Prerequisites

- Create or have an active Microsoft Azure account.
- Basic knowledge of cybersecurity and IT concepts:
  -  Virtual Machines
  -  SIEM concepts
  -  Firewalls
  -  Remote Desktop Connection
  -  Knowledge of query languages like SQL for KQL log analysis

## Table Of Contents

1. [Chapter 1: Creating The Azure Virtual Machine]()
2. [Chapter 2: Setting Up Azure Logs Analytics Workspace]()
3. [Chapter 3: Adding Microsoft Sentinel]()
4. [Chapter 4: First Look At New Virtual Machine]()
5. [Chapter 5: Creating SIEM Dashboard]()
6. [Chapter 6: Analyzing Logs in Azure with KQL]()
7. [Chapter 7: Findings and Conclusions]()

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- This project is directly inspired by Josh Madakor's [YouTube Channel](https://www.youtube.com/@JoshMadakor).
  - [Josh Madakor's Video Link](https://www.youtube.com/watch?v=RoZeVbbZ0o0)

- I appreciate [ZeroTrustAccess](https://github.com/ZeroTrustAccess) and their documentation on the same [project](https://github.com/ZeroTrustAccess/Honeypot/blob/main/README.md) for markdown layout inspiration and more. Their work was especially helpful as some Azure features have been updated or relocated since Josh Madakor’s video from over two years ago.

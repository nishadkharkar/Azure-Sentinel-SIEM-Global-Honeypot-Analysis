# Azure-Sentinel-SIEM-Global-Honeypot-Analysis
A cloud-native SIEM and Honeypot implementation using Microsoft Azure. Analyzes real-time RDP brute-force attacks by integrating a vulnerable Windows VM with Azure Sentinel and custom PowerShell automation to visualize global threat patterns.
# 🛡️ Azure Sentinel SIEM & Global Honeypot Analysis

A comprehensive security project demonstrating the implementation of a cloud-native SIEM (Security Information and Event Management) system to monitor, log, and visualize live cyber attacks. This project utilizes a "Honeypot" strategy to attract and analyze RDP brute-force attempts from around the world.

[![Azure](https://img.shields.io/badge/Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Microsoft Sentinel](https://img.shields.io/badge/Microsoft_Sentinel-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://azure.microsoft.com/en-us/products/microsoft-sentinel/)
[![Kusto](https://img.shields.io/badge/KQL-Kusto_Query-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)

---

## 🎯 Project Objectives

- **Simulate a High-Risk Environment**: Deploy a vulnerable Windows VM in Azure to attract real-world RDP brute-force attacks.
- **Automated Threat Intelligence**: Use PowerShell to extract attacker metadata (IP, Geolocation, ISP, and Username) from Windows Event Logs (**Event ID 4625**).
- **Centralized Monitoring**: Transform raw log data into actionable security intelligence using **Azure Log Analytics** and **Microsoft Sentinel**.
- **Visual Analytics**: Create a dynamic Sentinel Workbook to plot attack origins on a global map.

---

## 🛠️ Tech Stack & Architecture

- **Platform**: Microsoft Azure (Virtual Machines, Network Security Groups)
- **SIEM/Analytics**: Microsoft Sentinel, Azure Log Analytics Workspaces
- **Scripting**: PowerShell (Custom Log Exporter & API Integration)
- **API Integration**: IP-API.com (for geolocation enrichment)
- **Query Language**: KQL (Kusto Query Language)

### 📐 Logical Workflow
1. **VM Deployment**: Provisioned a Windows 10 VM with local firewalls and Network Security Group (NSG) rules set to "Allow-All" to maximize discoverability.
2. **Log Enrichment**: A custom PowerShell script continuously monitors failed RDP logins, extracts IPs, and queries a Geolocation API to append longitude, latitude, and country data.
3. **Log Ingestion**: Structured logs are sent to a custom Log Analytics Workspace.
4. **Analysis & Visualization**: Sentinel queries the workspace via KQL to generate live heatmaps of attack origins.

---

## 📊 Key Findings & Security Insights

- **Credential Patterns**: Analysis revealed that automated scripts prioritize default usernames like `ADMIN` and `administrator`, confirming the persistence of "low-hanging fruit" attack vectors.
- **Global Reach**: The system recorded attacks from multiple continents within hours of deployment, highlighting the velocity at which automated scanners identify vulnerable cloud assets.
- **ISP Trends**: Identified specific international ISPs frequently associated with malicious traffic, providing a baseline for potential IP-range blacklisting.

---

## 📂 Repository Contents

- `scripts/LogExporter.ps1`: The PowerShell automation used to parse Event Logs and fetch Geo-data.
- `kql/MapQuery.kql`: The Kusto query used to power the Sentinel Workbook map.
- `docs/`: Contains the final project report and screenshots of the SIEM Dashboard.

---

## 🎓 Academic Context
This project was developed at **George Mason University** (AIT 670) by Nishad Kharkar and team, focusing on cloud-native threat detection and the efficacy of honeypot-based security research.

---

### 📄 How to Use
1. Set up an Azure Subscription and Log Analytics Workspace.
2. Deploy a Windows VM and disable the firewall.
3. Run the provided PowerShell script on the VM.
4. Configure Microsoft Sentinel to ingest the custom log file.
5. Import the KQL query into a Sentinel Workbook to visualize the data.

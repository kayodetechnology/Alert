# Building a SOC + Honeynet in Azure (Live Traffic)


## Introduction


In this project, I focused on crafting and implementing Active Rules within Microsoft Sentinel Analytics.

- Azure Key Vault (Event Logs)
 This KQL code is querying Azure Diagnostics logs to identify and retrieve information about failed access attempts in Microsoft Key Vault where the result signature is "Forbidden". It's a useful query for monitoring and investigating access control issues in Azure Key Vault
![Azure Key Vault](https://i.imgur.com/umtvGLE.jpeg)

 
- Brute Force SUCCESS (Windows Event Logs)
  This KQL code helps identify potential brute force attacks by analyzing both failed and successful Windows logon events within the last hour and providing information about the combination of failed and successful logons based on common attributes like IP address and destination host name.
  ![Brute Force SUCCESS - Windows](https://i.imgur.com/RsI4LOc.jpeg)


- Brute Force ATTEMPT (Azure Active Directory Event Logs)
   This KQL code is querying Sign-in logs to extract information about failed sign-in attempts where the result description indicates issues related to invalid usernames or passwords. The projected fields provide details about the sign-in event, including user information, IP address, and location details.
  ![Brute Force ATTEMPT](https://i.imgur.com/H58Xc7Q.jpeg)

- Brute Force ATTEMPT (MS SQL Server Event Logs)
  This KQL code is querying events from the Application log to identify potential brute force attempts on a Microsoft SQL Server. It focuses on events with a specific EventID related to login failures, extracts the attacker's IP address, and summarizes the failures by IP address and destination host name, filtering for cases where the failure count is 10 or more.
![Brute Force ATTEMPT](https://i.imgur.com/8i2eLVu.jpeg)
  
- SecurityAlert (Malware Detected Log Analytics Alerts Events)
  So, the overall purpose of this query is to retrieve events from the Windows Defender operational log where the scan process has either started (Event ID 1116) or completed (Event ID 1117). It helps monitor and analyze Windows Defender scan activities on the system.
  ![Malware Detected](https://i.imgur.com/bnz8Za2.jpeg)
  
- Brute Force ATTEMPT (Linux Syslog Server Event Logs)
  This KQL code is querying syslog events from a Linux system to identify potential brute force attempts by focusing on authentication-related events with failed password attempts. It extracts the attacker's IP address and summarizes the failures by IP address, destination host name, and destination IP, filtering for cases where the failure count is 10 or more.
   ![Linux Syslog](https://i.imgur.com/rcmeZVw.jpeg)

 - Brute Force ATTEMPT (Windows VM Event Logs)
   This KQL code is querying SecurityEvent logs to identify instances of failed logon attempts (Event ID 4625) within the last hour. It then summarizes these events based on the attacker's IP address, event ID, activity, and destination host name, filtering for cases where the failure count is 10 or more. This can be useful for detecting and investigating potential security threats or unauthorized access attempts.
![Windows Vm](https://i.imgur.com/oQfrcDh.jpeg)

- Possible Privilege Escallation (Global Administrator Role Assignment)
  This KQL code is querying audit logs to identify successful operations where a user is added to a role, specifically focusing on roles like "Global Administrator" or "Company Administrator." The projected fields provide details about the event, including the timestamp, operation name, assigned role, result status, target resources, initiator ID, and target ID. This type of query is useful for monitoring and auditing role assignments in a security or compliance context.
  ![G-Admin](https://i.imgur.com/ajkQAuA.jpeg)


- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/6OCnR9P.jpeg)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/NB5dp26.jpeg)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/o2JOTlc.jpeg)<br>
![MSSQL Auth Failures](https://i.imgur.com/0BmVMDq.jpeg)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-02-27T17:17:56.9449504Z
Stop Time  2024-02-28T17:17:56.9449504Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 33039
| Syslog                   | 6721
| SecurityAlert            | 189
| SecurityIncident         | 1299
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I established a miniature honeynet using Microsoft Azure, integrating log sources into a Log Analytics workspace. The orchestration of alerts and incidents was executed through Microsoft Sentinel, utilizing the ingested logs. Furthermore, metrics were initially gauged in an insecure environment before the enforcement of security controls. Subsequently, a follow-up measurement was conducted post-implementation of security measures. Notably, the application of security controls (NIST 800-53) resulted in a significant reduction in both security events and incidents, underscoring their efficacy.

It is essential to highlight that if the network resources experienced substantial utilization by regular users, there could have been a likelihood of generating more security events and alerts within the 24-hour period following the deployment of security controls.

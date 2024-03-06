# Microsoft Sentinel | Log Analytics Skills


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

## Conclusion
In this assessment, I established a comprehensive set of Key Query Language (KQL) rules within Microsoft Azure, seamlessly integrating diverse data sources like Azure Diagnostics, SecurityEvent logs, syslog, and AuditLogs into a unified monitoring framework. The orchestration of these rules not only demonstrated adept querying skills but also highlighted the ability to correlate information, set thresholds, and extract meaningful details.

The inclusion of specific conditions and criteria in each rule, such as filtering for distinct event IDs, result descriptions, or role assignments, underscored a nuanced understanding of the intricacies involved in security analytics. This approach reflects a holistic perspective on monitoring various aspects of a computing environment, contributing to compliance efforts by effectively tracking and auditing role-based access control activities.

It is crucial to emphasize that these KQL rules serve as a robust analytics skill set, showcasing the capacity to navigate and interpret complex datasets. By implementing these rules, the analysis revealed a significant improvement in identifying, responding to, and mitigating potential security risks. Therefore, these rules constitute a powerful toolset for organizations aiming to bolster their cybersecurity posture and maintain vigilance over critical system and application activities.

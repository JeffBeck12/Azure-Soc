# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)



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
![image](https://github.com/JeffBeck12/Azure-Soc/assets/138726687/72f133c0-0116-43ff-839c-6d3bb9b64e80)
![image](https://github.com/JeffBeck12/Azure-Soc/assets/138726687/7a56355e-b7a9-4d8c-8ef8-1938d4acc749)
![image](https://github.com/JeffBeck12/Azure-Soc/assets/138726687/06701f55-8d1a-49db-a913-0f83704c0617)
![image](https://github.com/JeffBeck12/Azure-Soc/assets/138726687/42708a96-d63a-4094-88dd-dfaec13cf28d)



## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 52480
| Syslog                   | 16158
| SecurityAlert            | 10
| SecurityIncident         | 359
| AzureNetworkAnalytics_CL | 1701

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 285
| Syslog                   | 21
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Performed a security Audit 
TO: IT Manager, stakeholders

FROM: Jeffrey Beckett

DATE: 06/29/2023

SUBJECT: Internal IT Audit Findings and Recommendations


Dear Colleagues,

I would like to bring your attention to the findings and recommendations from the recent internal IT audit conducted at Botium Toys. The audit focused on assessing the security posture, compliance alignment, and technology inventory of our organization. Below, you will find a summary of the audit scope, goals, critical findings, and a concise summary of our recommendations.

Audit Summary:

Scope: The audit covered user permissions, controls implementation, procedures and protocols, compliance alignment, and technology inventory at Botium Toys.
Goals: Enhance security posture, achieve compliance, establish a robust cybersecurity framework, implement least privilege, develop comprehensive procedures and protocols, and maintain an updated technology inventory.
Critical Findings:
The audit identified the following critical findings:

User Permissions: Inconsistencies in user permissions across systems, posing a risk of unauthorized access.
Controls Implementation: Gaps in controls related to accounting, endpoint detection, firewalls, intrusion detection systems, and SIEM tools.
Compliance Alignment: Current user permissions, controls, procedures, and protocols do not fully align with necessary compliance requirements.
Control of Least Privilege and Separation of Duties
Disaster recovery plans
Password, access control, and account management policies, including the implementation of a password management system
Encryption (for secure website transactions)
IDS (Intrusion Detection System)
Backups
AV software
CCTV (Closed-Circuit Television)
Locks
Manual monitoring, maintenance, and intervention for legacy systems
Fire detection and prevention systems
Policies need to be developed and implemented to meet PCI DSS and GDPR compliance requirements.
Policies need to be developed and implemented to align to SOC1 and SOC2 guidance related to user access policies and overall data safety.
Other Findings:
In addition to the critical findings, the audit revealed the following areas requiring improvement:

Procedures and Protocols: Existing procedures and protocols for accounting, endpoint detection, firewalls, intrusion detection systems, and SIEM tools.
Technology Inventory: Incomplete documentation of hardware and system access.
Time-controlled safe
Adequate lighting
Locking cabinets
Signage indicating alarm service provider
Summary and Recommendations:
To address these findings and strengthen our IT security, the following actions are recommended:

Implement the principle of least privilege and conduct regular reviews of user permissions.
Enhance controls by adopting industry best practices such as multi-factor authentication, patch management, and network segmentation.
Develop comprehensive procedures and protocols that address specific security requirements, incident response, and change management processes.
Maintain an updated inventory of technology assets to ensure accurate visibility and control.
Develop and implement policies to meet PCI DSS and GDPR compliance requirements.
Develop and implement policies to align with SOC1 and SOC2 guidance related to user access policies and overall data safety.
Address the additional findings by implementing time-controlled safes, ensuring adequate lighting, using locking cabinets, and displaying signage indicating the alarm service provider.
By implementing these recommendations, we will enhance our security posture, achieve compliance, and establish a robust cybersecurity framework to protect our critical assets and ensure business continuity.


## CyberSecurity Incident Reports 


Section 1: Identify the type of attack that may have caused this 
network interruption

After reviewing the logs in my opinion the website is being Dos attacked. The server is being bombarded with SYN requests causing the server to stop responding. This could be what is called a SYN attack.
 

Section 2: Explain how the attack is causing the website to malfunction
When the website visitors try to establish a connection with the web server, a
three-way handshake occurs using the TCP protocol. The handshake consists
of three steps:
1. A SYN packet is sent from the source to the destination, requesting to
connect.
2. The destination replies to the source with a SYN-ACK packet to accept
the connection request. The destination will reserve resources for the
source to connect.
3. A final ACK packet is sent from the source to the destination
acknowledging the permission to connect.

A SYN flood attack simulates a TCP connection and floods the server with SYN packets. The attacker floods the target server with a high volume of SYN requests, overwhelming its resources and causing a disruption in normal operations.
Initially, the attacker’s SYN request is answered normally by the web server (log items 52-54). However, the attacker keeps sending more SYN requests. The log begins to reflect the struggle the web server is having to keep up with the abnormal number of SYN requests coming in at a rapid pace. The attacker is sending several SYN requests every second. Eventually the Server  stopped responding to  legitimate employee visitor traffic.



## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.

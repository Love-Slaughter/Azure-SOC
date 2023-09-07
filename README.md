# Azure Cloud SOC with Honeynet Implementation (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

I built a scaled-down honeynet in Azure that ingests log sources from various resources into a Log Analytics workspace. These logs are then used by Microsoft Sentinel to populate attack maps, trigger alerts, and create incidents. Security metrics were taken before and after hardening to demostrate successful hardening capablitlites. 
**This is smaller verison made for demonstration purposes**

## Some tools used
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture in Azure consisted of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

"Before" metrics were resources intentionally left vulnerable to the internet.   
"After" metrics are of the very same resources after applying hardening stradgies such as firewall rules and NSG configuration. 


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](<img width="844" alt="Before-nsg-malicious-allowed-in" src="https://github.com/Love-Slaughter/Azure-SOC/assets/132439251/a8527ae5-b182-4a12-80dc-7a5c976cfacf">
)<br>
![Linux Syslog Auth Failures](<img width="738" alt="Before-linux-sssh-auth-failures" src="https://github.com/Love-Slaughter/Azure-SOC/assets/132439251/a02fa4d8-8ea8-4122-993b-e4b072e7d2ce">
)<br>
![Windows RDP/SMB Auth Failures](<img width="762" alt="Before-windows-rdp-smb-auth-failures" src="https://github.com/Love-Slaughter/Azure-SOC/assets/132439251/bfc2f188-c18a-4d03-850b-835e65e33eea">
)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
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

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.

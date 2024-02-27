# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/9qNFLsZ.png)

## Introduction

In this undertaking, I constructed a compact honeynet within the Azure framework. I gathered log data from diverse sources and funneled it into a Log Analytics workspace. Subsequently, Microsoft Sentinel utilized this workspace to generate attack maps, initiate alerts, and formulate incidents. I assessed security metrics within the vulnerable environment over a 24-hour period, implemented security controls to fortify the environment, reevaluated metrics for an additional 24 hours, and present the outcomes below. The showcased metrics include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://imgur.com/vZuNxfw.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://imgur.com/cpUtr4y.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 window, 1 linux, 1 SQL Database)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://imgur.com/0S5lz3e.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/SyLMQ8o.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/kPuWG6i.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-01-14 3:15:56 PM
Stop Time 2023-03-15 3:15:56 PM

![Screen Shot 2024-01-21 at 11 19 31 PM](https://github.com/alfonsonyc2005/Azure-SOC/assets/141835414/ac205dda-ee70-4cc3-90cd-46d1b35859a4)

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-01-18 10:17:06 PM
Stop Time	2024-01-19 10:17:06 PM

![Screen Shot 2024-01-21 at 11 20 24 PM](https://github.com/alfonsonyc2005/Azure-SOC/assets/141835414/3a4f9caa-2bb9-4119-8cee-f902a406a63a)

## Conclusion

In this project, a miniature honeynet was established within Microsoft Azure, and various log sources were seamlessly integrated into a Log Analytics workspace. The deployment of Microsoft Sentinel played a crucial role in initiating alerts and generating incidents based on the assimilated logs. Furthermore, metrics were assessed in the insecure environment both before the implementation of security controls and after their application. It is noteworthy that the implementation of security measures resulted in a significant reduction in the number of security events and incidents, highlighting the efficacy of these controls.

Importantly, if the network resources had been extensively utilized by regular users, it is plausible that a higher volume of security events and alerts might have been produced in the 24-hour period following the implementation of the security controls.

# Azure SOC + Honeynet: Live Attack Telemetry and Hardening Impact

## Overview
This project demonstrates the deployment of a **cloud-based honeynet in Microsoft Azure** to observe real-world attack traffic, analyze security telemetry, and measure the impact of security hardening controls.

A deliberately exposed environment was monitored for 24 hours using **Microsoft Sentinel and Log Analytics**, then secured using network and platform protections. Metrics were collected again to evaluate the effectiveness of those controls.

---

## Architecture
### Before Hardening (Exposed)
![Architecture Before Hardening](https://imgur.com/vZuNxfw.jpg)

### After Hardening (Secured)
![Architecture After Hardening](https://imgur.com/cpUtr4y.jpg)

---

## Technologies Used
- Microsoft Azure
- Microsoft Sentinel
- Log Analytics Workspace
- Azure Virtual Network (VNet)
- Network Security Groups (NSGs)
- Azure Private Endpoints
- Windows & Linux Virtual Machines
- Azure SQL Database
- Azure Key Vault
- Azure Storage Account

---

## Honeynet Design
The honeynet consisted of intentionally exposed cloud resources designed to attract and log malicious activity:

- Virtual Network with public-facing resources
- Windows VM (RDP exposed)
- Linux VM (SSH exposed)
- Azure SQL Database
- Centralized logging via Log Analytics
- Microsoft Sentinel for alerting and incident creation

**Objective:** Capture live attack telemetry and analyze attacker behavior.

---

## Telemetry Collected
The following log sources were ingested and analyzed:

- `SecurityEvent` – Windows Event Logs
- `Syslog` – Linux authentication and system logs
- `SecurityAlert` – Sentinel-triggered alerts
- `SecurityIncident` – Sentinel incidents
- `AzureNetworkAnalytics_CL` – NSG flow logs showing malicious traffic

---

## Metrics: Before Hardening
**Duration:** 24 hours  
**Environment State:** Fully exposed to the internet

### Observations
- High volume of inbound malicious traffic
- Repeated authentication attempts against Windows and Linux VMs
- Numerous Sentinel alerts and incidents generated

### Attack Visualizations
![NSG Malicious Flows](https://imgur.com/0S5lz3e.png)  
![Linux Auth Failures](https://imgur.com/SyLMQ8o.png)  
![Windows RDP/SMB Failures](https://imgur.com/kPuWG6i.png)

<details>
<summary><strong>Metric details (Before Hardening)</strong></summary>

- NSGs allowed unrestricted inbound traffic
- Public endpoints enabled on all resources
- No Private Endpoints or IP restrictions
- Sentinel actively detected and correlated attack activity

</details>

---

## Security Hardening 
The environment was secured using layered defensive controls:

- NSGs restricted to allow traffic **only from admin workstation**
- Public access removed where possible
- Azure Private Endpoints enabled
- Resource firewalls enforced

**Objective:** Reduce attack surface and validate security control effectiveness.

---

## Metrics: After Hardening
**Duration:** 24 hours  
**Environment State:** Hardened and restricted

### Observations
- No malicious inbound traffic detected
- No authentication attacks recorded
- Sentinel attack maps returned no results
- Zero security incidents generated

```text
All Sentinel map queries returned no results due to the absence of malicious activity.


# 🛡️ Splunk Huawei Firewall Security Monitoring & Analytics Home Lab

## 🎯 Project Objective
On my project, I used Splunk as our central observability hub to gain centralized visibility into network traffic and detect potential security threats. By analyzing network traffic, login attempts, and firewall logs all at once, Splunk can raise an alarm if an unauthorized user is trying to breach the system. This allows security operations teams to proactively identify perimeter risks instead of digging through manual flat-file logs.

---

## 🛠️ Project Implementation Details

### 1. Forwarder & Data Ingestion Setup
- Configured and deployed **Splunk Universal Forwarders** to securely collect and stream live firewall syslog data into a centralized Splunk index.
- Onboarded the unstructured log streams by creating dedicated field structures and assigning a custom `huawei:firewall` sourcetype.

### 2. Threat Hunting & Normalization (SPL)
- Standardized data fields to perfectly align with the **Splunk Common Information Model (CIM)**. This ensures fields like `src_ip` and `action=blocked` parse universally regardless of the hardware.
- Crafted optimized Search Processing Language (SPL) queries to isolate volumetric denial spikes, active port scans, and unauthorized connection requests.

```splunk
index=firewall01_log sourcetype="huawei:firewall"
| stats count by PolicyName
| sort - count
```
*Explanation:* This tells Splunk to look at network logs from the firewall, find all connections, count how many times each policy was triggered (like `MGMT-DENY`), and sort them to see the top security policy hits immediately.

### 3. Platform Security & Identity Governance (RBAC)
- Demonstrated platform security best practices by implementing strict **Role-Based Access Control (RBAC)**.
- Created custom user restrictions to separate root system administrative actions from standard operations, assigning tiered capabilities to a dedicated `security_analyst` role to enforce the Principle of Least Privilege.

---

## ⚡ Business Impact & Portfolio Value
* **Unified Ecosystem Visibility:** Successfully aggregated disparate network boundaries into a single pane of glass, removing host log fragmentation.
* **Proactive Defense Stance:** Shifted monitoring methodologies from reactive forensic investigation to dynamic, real-time alerting mechanisms.
* **Optimizing Alert Triage:** Drastically dropped Mean Time to Detection (MTTD) by providing pre-parsed mapping parameters for rapid analytical pivoting.

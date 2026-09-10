# 🛡️ Splunk Huawei Firewall Security Monitoring & Analytics Home Lab

## 🎯 Project Objective
On my project, I used Splunk as our central observability hub to gain centralized visibility into network traffic and detect potential security threats. By analyzing network traffic, login attempts, and firewall logs all at once, Splunk can raise an alarm if an unauthorized user is trying to breach the system. This allows security operations teams to proactively identify perimeter risks instead of digging through manual flat-file logs.

---

## 🛠️ Step 1: Forwarder & Data Ingestion Setup
I deployed and configured Splunk Universal Forwarders to securely collect and stream live firewall syslog data into a centralized Splunk index.

### 📋 Ingestion & Source Type Metrics
Here is the tracking snapshot where the unstructured logs are onboarding with the assigned `huawei:firewall` sourcetype configurations:

<img src="https://githubusercontent.com" width="650px"/>

*Setting up the index parameters and establishing the `firewall01_log` storage bucket:*
<img src="https://githubusercontent.com" width="650px"/>

---

## 🔍 Step 2: Threat Hunting & Normalization (SPL)
I performed basic searches using **SPL (Search Processing Language)**, applied filters, and used statistical commands to track denied traffic and potential reconnaissance attacks. I ensured that data collected from network firewalls was explicitly mapped to the **Splunk Common Information Model (CIM)** so fields like `src_ip` and `action=blocked` parse universally across the platform.

### Implemented Threat Hunting Query:
```splunk
index=firewall01_log sourcetype="huawei:firewall"
| stats count by PolicyName
| sort - count
```
*Explanation:* This tells Splunk to look at network logs from the firewall, find all connections, count how many times each policy was triggered (like `MGMT-DENY`), and sort them to see the top policy violations instantly.

---

## 📊 Step 3: Security Operations Center (SOC) Dashboard
I compiled the analyzed traffic data and statistical metrics into an interactive dashboard to give the security engineering team real-time visibility into active perimeter distributions.

<img src="https://githubusercontent.com" width="650px"/>

---

## 🔒 Step 4: Security Best Practices & RBAC Roles
To demonstrate platform security best practices, I implemented strict **Role-Based Access Control (RBAC)**. I provisioned a dedicated `security_analyst` role to enforce the Principle of Least Privilege, isolating user access permissions to protect critical system assets.

<img src="https://githubusercontent.com" width="650px"/>

---

## ⚡ Business Impact & Results
* **Centralized Security View:** Consolidated all isolated network firewall syslogs into a single pane of glass for real-time traffic monitoring.
* **Proactive Defense:** Enabled rapid security alert triage for malicious brute-force or port scanning trends.
* **Data Security & Compliance:** Enforced strict index segregation and access controls to keep sensitive infrastructure logs isolated and safe.

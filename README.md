# 🛡️ Splunk Huawei Firewall Security Monitoring & Analytics

## 🎯 Objective (Context)
In modern corporate networks, security data is often siloed inside standalone network devices, making it incredibly difficult to track cyber threat progressions. I built this home lab project to establish centralized observability over perimeter security infrastructure. By streaming live firewall logs into an enterprise SIEM architecture, this framework enables a Security Operations Center (SOC) team to proactively capture, analyze, and neutralize perimeter risks in real-time, replacing slower manual log verification patterns.

---

## 🛠️ Project Implementation (Action)

### 1. Forwarder & Ingestion Architecture
Deployed and configured a Splunk Universal Forwarder agent to monitor target directories, packaging raw firewall syslogs seamlessly over an encrypted TCP stream to a central Splunk indexer. 

![Splunk Universal Forwarder Configuration](forwarder.png)

### 2. Data Classification & Indexing
Onboarded the unstructured log streams by creating dedicated field structures, assigning a custom `huawei:firewall` sourcetype, and mapping traffic to a segregated index (`index=firewall01_log`) with a strict 90-day retention pattern.

![Splunk Ingestion Review and Index Setup](ingestion.png)

### 3. Threat Hunting & Normalization
Utilized Search Processing Language (SPL) to normalize arbitrary network traffic details to line up precisely with the **Splunk Common Information Model (CIM)**. I crafted targeted search queries designed to isolate volumetric denial spikes, active port scans, and suspicious geographic endpoints:

```splunk
index=firewall01_log sourcetype="huawei:firewall" "DROP"
| stats count by PolicyName
| sort - count
```

---

## 📊 Security Operations Center (SOC) Dashboard
Integrated all streaming query statistics into an interactive, high-visibility **Huawei Firewall Security Dashboard**. This interface highlights real-time policy distributions (such as `MGMT-DENY` vs. `OUTSIDE-IN-ALLOW`), enabling analysts to immediately spot perimeter scanning threats.

![Huawei Firewall Security Dashboard](dashboard.png)

---

## 🔒 Platform Security & Identity Governance (RBAC)
Demonstrated platform engineering best practices by implementing strict Role-Based Access Control (RBAC). Created custom user restrictions to separate root system administrative actions from standard operations, assigning tiered capabilities to the dedicated `security_analyst` role to enforce the Principle of Least Privilege.

![Splunk RBAC Roles and User Configuration](rbac.png)

---

## ⚡ Business Impact & Portfolio Value (Result)
* **Unified Ecosystem Visibility:** Successfully aggregated disparate network boundaries into a single pane of glass, removing host log fragmentation.
* **Proactive Defense Stance:** Shifted monitoring methodologies from reactive forensic investigation to dynamic, real-time alerting mechanisms.
* **Optimized Incident Management:** drasitcally dropped Mean Time to Detection (MTTD) by providing pre-parsed mapping parameters (`src_ip`, `dest_port`) for rapid analytical pivoting.

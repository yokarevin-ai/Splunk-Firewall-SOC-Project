# Splunk Firewall Security Monitoring & Analytics

## 🎯 Objective (Context)
In modern corporate environments, security data is often trapped inside isolated devices, making it incredibly difficult to spot active cyber threats. I built this project to establish centralized visibility over our network perimeter. By streaming firewall logs into Splunk, this setup allows a Security Operations Center (SOC) team to proactively detect potential security breaches and malicious activity across the network in real time, rather than manually hunting through flat text files.

## 🛠️ What I Did (Action)
* **Data Ingestion:** Configured and deployed Splunk Universal Forwarders to securely collect and stream live firewall syslog data into a centralized Splunk index.
* **Data Normalization:** Normalized unstructured log data to perfectly align with the **Splunk Common Information Model (CIM)**. This ensures fields like `src_ip`, `dest_port`, and `action=blocked` are universally searchable regardless of the firewall vendor.
* **Threat Hunting:** Authored optimized Search Processing Language (SPL) queries to analyze spikes in denied traffic, helping isolate port scans, brute-force attempts, and unauthorized connection requests.
* **Security Best Practices:** Applied the Principle of Least Privilege by isolating data into dedicated indexes and designing efficient queries that limit search scope to protect system resources.

## ⚡ Impact (Result)
This implementation successfully transforms raw, unreadable machine data into actionable security intelligence. It enables SOC teams to proactively identify and flag perimeter risks immediately as they occur. By replacing manual log aggregation with centralized Splunk dashboards, this framework significantly reduces the Mean Time to Detection (MTTD) from hours to seconds, allowing analysts to defend critical internal assets faster.

# SIEM Log Triage & Dual-File Incident Parsing

## Overview
This automated Python script parses raw SIEM network traffic logs and correlates telemetry entries against a central IP blocklist and risk classification thresholds. It separates anomalous or critical events from normal traffic, writes dedicated output logs, and generates a structured incident report for SOC operations.

---

## Technical Features
- **Dual-Source Ingestion**: Dynamically imports raw network traffic entries and IP blocklist databases[cite: 2].
- **Correlation & Triage Engine**: Applies multi-condition filtering logic to evaluate both source IP reputation and threat severity levels (`CRITICAL`)[cite: 2].
- **Automated Incident Logging**: Writes flagged security events to `incident_report.log` while writing verified traffic to `cleared_traffic.log`[cite: 2].
- **Executive Triage Summary**: Prints real-time metrics summarizing processed events, quarantined threats, and cleared connections[cite: 2].

---

## System Workflow & Logic

1. **Telemetry & Threat Feed Ingestion**: Loads raw traffic logs (`raw_traffic.log`) containing `IP|User|Risk_Level` tuples alongside active threat intelligence blocklists (`ip_blocklist.txt`)[cite: 2].
2. **Conditional Parsing**:
   - Each traffic entry is split using the delimiter `|` into `ip_add`, `user`, and `risk`[cite: 2].
   - **Quarantine Logic**: Flagged if `ip_add` exists in `ip_blocklist.txt` **OR** `risk` level is explicitly marked as `CRITICAL`[cite: 2].
3. **Log Writing & Output**: Generates clean output files for downstream ingestion or further analyst investigation[cite: 2].

---

## Python Script Implementation

```python
# Initialize data inputs and file structures
traffic_entries = "192.168.1.10|alice|LOW 10.0.0.99|admin|CRITICAL 192.168.1.45|bob|LOW 172.16.0.15|unknown|HIGH 192.168.1.88|charlie|LOW 10.0.0.99|service_acc|CRITICAL"
blocked_ips = "10.0.0.99 203.0.113.55 198.51.100.4"
incident_list = []
cleared_list = []

# Write initial mock telemetry and blocklist feeds
with open("raw_traffic.log", "w") as file:
    file.write(traffic_entries)

with open("ip_blocklist.txt", "w") as file:
    file.write(blocked_ips)

# Import logs for automated analysis
import_raw = "raw_traffic.log"
import_ip = "ip_blocklist.txt"

with open(import_raw, "r") as file:
    raw = file.read()

with open(import_ip, "r") as file:
    ip = file.read()

raw = raw.split()
blocked_ips = blocked_ips.split()

print("Traffic Entries:", raw)
print("Blocked IPs:", blocked_ips)
print()

# Parse telemetry and evaluate risk conditions
for element in raw.copy():
    parts = element.split("|")
    ip_add = parts[0]
    user = parts[1]
    risk = parts[2]

    # Evaluate against IP blocklist or critical risk flag
    if ip_add in blocked_ips or risk == "CRITICAL":
        incident_list.append(element)
    else:
        cleared_list.append(element)

# Format outputs
incident_str = " ".join(incident_list)
cleared_str = " ".join(cleared_list)

# Write updated logs
with open("incident_report.log", "w") as file:
    file.write(incident_str)

with open("cleared_traffic.log", "w") as file:
    file.write(cleared_str)

# Console Summary Output
print("--- REPORT ---")
print(f"Total Events Processed: {len(raw)}")
print(f"Total Incidents Quarantined: {len(incident_list)}")
print(f"Total Clean Entries: {len(cleared_list)}")
print("Incidents:", incident_str)
print("Cleared:", cleared_str)
```

### Terminal Execution Log
```text
Traffic Entries: ['192.168.1.10|alice|LOW', '10.0.0.99|admin|CRITICAL', '192.168.1.45|bob|LOW', '172.16.0.15|unknown|HIGH', '192.168.1.88|charlie|LOW', '10.0.0.99|service_acc|CRITICAL']
Blocked IPs: ['10.0.0.99', '203.0.113.55', '198.51.100.4']

--- REPORT ---
Total Events Processed: 6
Total Incidents Quarantined: 2
Total Clean Entries: 4
Incidents: 10.0.0.99|admin|CRITICAL 10.0.0.99|service_acc|CRITICAL
Cleared: 192.168.1.10|alice|LOW 192.168.1.45|bob|LOW 172.16.0.15|unknown|HIGH 192.168.1.88|charlie|LOW

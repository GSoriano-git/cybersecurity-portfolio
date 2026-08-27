# Incident Report Analysis: DoS Attack via ICMP Packet Flood

## 📌 Scenario Background

As a Cybersecurity Analyst for a multimedia company providing web design, graphic design, and social media marketing solutions, I investigated a recent security event that caused a two-hour internal network outage.

An external malicious actor exploited an unconfigured firewall to launch a Denial of Service (DoS) attack via an ICMP packet flood. The massive influx of ICMP pings overwhelmed network capacity, rendering internal resources and normal network traffic inaccessible.

### Key Incident Response & Remediation Actions
* **Immediate Mitigation:** Blocked incoming ICMP packets, took non-critical services offline, and prioritized restoring critical network operations.
* **Root Cause:** An unconfigured firewall permitted unchecked incoming ICMP traffic without rate limiting or source verification.
* **Preventive Controls Implemented:**
  * Configured firewall rate-limiting for incoming ICMP packets.
  * Enabled source IP verification to detect and block spoofed addresses.
  * Deployed Intrusion Detection/Prevention Systems (IDS/IPS) to filter suspicious traffic.
  * Integrated network monitoring software for continuous anomaly detection.

*This analysis documents the incident lifecycle and long-term security strategy using the **NIST (National Institute of Standards and Technology) Cybersecurity Framework (CSF)**.*

---

## 🛡️ NIST Cybersecurity Framework (CSF) Analysis

> **What is NIST?**  
> **NIST** stands for the **National Institute of Standards and Technology**, a non-regulatory agency of the U.S. Department of Commerce. The **NIST Cybersecurity Framework (CSF)** provides industry-standard guidelines, best practices, and controls to help organizations manage and reduce cybersecurity risks across five core functions: *Identify, Protect, Detect, Respond, and Recover*.

| NIST CSF Function | Incident Analysis Details |
| :--- | :--- |
| **Summary** | The organization experienced a security event when the internal network shut down for two hours. The cybersecurity team discovered the disruption was caused by a Denial of Service (DoS) attack via an ICMP packet flood exploiting an unconfigured firewall. The team responded by blocking the attack and stopping non-critical network services so that critical network services could be restored. |
| **Identify** | The cybersecurity team performed an investigation to pinpoint the cause of the security event. A threat actor deployed an ICMP flood attack through the company network’s unconfigured firewall, resulting in a Denial of Service (DoS) attack that affected the entire internal network. |
| **Protect** | The team implemented security methods to prevent recurrence, including configuring the firewall to limit the rate of incoming ICMP packets and placing an IDS/IPS between the internal network and firewall to mitigate suspicious traffic. |
| **Detect** | Implemented source IP address verification at the firewall to detect spoofed IP addresses and deployed network monitoring software to detect abnormal traffic patterns. |
| **Respond** | To mitigate future incidents, the team will isolate affected systems using network segmentation to contain attacks within specific subnets, restore disrupted services, analyze network logs for traffic anomalies, and report incidents to upper management and legal authorities as applicable. |
| **Recover** | Restored access to network services to a normal functioning state by blocking external ICMP floods at the firewall and pausing non-critical network services. Critical network services were restored first, followed by gradually bringing non-critical systems back online while continuously monitoring incoming ICMP traffic. |

---

### 📝 Reflections & Key Takeaways
Applying the NIST CSF framework demonstrates how combining proactive perimeter defenses (firewall rules, IDS/IPS) with clear incident response procedures minimizes operational downtime and protects business-critical resources.

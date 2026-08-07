**Incident report analysis**

**Scenario Background**

**As a Cybersecurity Analyst for a multimedia company providing web design, graphic design, and social media marketing solutions, I investigated a recent security event that caused a two-hour internal network outage.**

**An external malicious actor exploited an unconfigured firewall to launch a Denial of Service (DoS) attack via an ICMP packet flood. The massive influx of ICMP pings overwhelmed network capacity, rendering internal resources and normal network traffic inaccessible.**

**Key Incident Response & Remediation Actions:**

* **Immediate Mitigation: Blocked incoming ICMP packets, took non-critical services offline, and prioritized restoring critical network operations.**  
* **Root Cause: An unconfigured firewall permitted unchecked incoming ICMP traffic without rate limiting or source verification.**  
* **Preventive Controls Implemented:**  
  * **Configured firewall rate-limiting for incoming ICMP packets.**  
  * **Enabled source IP verification to detect and block spoofed addresses.**  
  * **Deployed Intrusion Detection/Prevention Systems (IDS/IPS) to filter suspicious traffic.**  
  * **Integrated network monitoring software for continuous anomaly detection.**

***This analysis documents the incident lifecycle and long-term security strategy using the NIST Cybersecurity Framework (CSF).***

| Summary | The organization experienced a security event when the internal network shut down for two hours. The cybersecurity team discovered the disruption was caused by a Denial of Service (DoS) attack via an ICMP packet flood exploiting an unconfigured firewall. The team responded by blocking the attack and stopping non-critical network services so that critical network services could be restored. |  |  |
| :---- | :---- | ----- | ----- |
| Identify | The cybersecurity team has performed an investigation to pinpoint the cause of the security event. It turns out that the threat actor has deployed an ICMP flood attack through the company network’s unconfigured firewall, resulting in a Denial of Service attack (DoS). The incident has affected the entire internal network of the company. |  |  |
| Protect | The team has implemented various security methods to prevent this security event from reoccurring. These are configuring the firewall by limiting the rate of incoming ICMP packets to the network. Lastly, an IDS/IPS placed between the internal network and the firewall to mitigate suspicious incoming traffic. |  |  |
| Detect | Verification on the source IP address in the firewall to check for any spoofed IP addresses. And a network monitoring software to detect abnormal traffic patterns.  |  |  |
| Respond | To mitigate future security incidents, the cybersecurity team must isolate the affected system through a network segmentation to prevent the spread of an attack to contain it within that specific subnet only. They will also attempt to restore the affected services and systems disrupted by the event. The team will need to analyze network logs to check for abnormal traffic patterns. The team will also report all incidents to the upper management and legal authorities, if applicable. |  |  |
| Recover | To recover from an ICMP flood attack, access to network services must be restored to a normal functioning state. External ICMP flood attacks will be blocked at the firewall, and non-critical network services will be stopped to reduce internal network traffic. Critical network services will be restored first, followed by gradually bringing non-critical network systems and services back online while continuously monitoring incoming ICMP traffic.  |  |  |

---


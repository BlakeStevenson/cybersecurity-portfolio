## Incident Report Analysis

### **Summary**
The company experienced a major security event when all network services suddenly became unresponsive. The cybersecurity team determined that the outage was caused by a distributed denial-of-service (DDoS) attack involving a large volume of incoming ICMP packets. The team mitigated the attack by blocking the malicious traffic and shutting down non-critical network services so that critical services could be restored.

---

### **Identify**
A malicious actor (or group) launched an ICMP flood attack that targeted the organization’s internal network. The attack impacted the entire environment, requiring all critical network resources to be secured and brought back online.

---

### **Protect**
The cybersecurity team added a firewall rule to rate-limit incoming ICMP packets and deployed an IDS/IPS solution to filter ICMP traffic exhibiting suspicious behavior.

---

### **Detect**
To improve detection capabilities, the team enabled source IP verification on the firewall to identify spoofed traffic. They also implemented network monitoring tools to alert on abnormal traffic patterns and spikes.

---

### **Respond**
For future incidents, the cybersecurity team plans to isolate affected systems to prevent further disruption, prioritize the restoration of critical services, and review network logs for malicious indicators. They will also ensure all incidents are reported to senior leadership and legal authorities when necessary.

---

### **Recover**
Recovery from an ICMP-based DDoS attack requires restoring access to network services and re-establishing normal operations. External ICMP floods should be blocked at the firewall, and non-critical services should be temporarily shut down to reduce internal load. Critical services should be brought online first, followed by the gradual restoration of non-critical services once the attack traffic dissipates.

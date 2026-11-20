# Snort Lab Project: Hands-On Network Monitoring, Intrusion Detection and Custom IDS Rules

## Project Overview

This project documents my hands-on experience using **Snort**, an open-source network intrusion detection and prevention system (IDS/IPS).

The lab was completed in a controlled virtual machine sandbox environment. Its purpose was to understand how network traffic can be monitored, analyzed and matched against detection rules to generate security alerts.

As an aspiring SOC Analyst, I wanted to gain practical experience with network monitoring, intrusion detection and basic alert investigation.

## Lab Objectives

- Understand the difference between IDS and IPS.
- Explore Snort and its operating modes.
- Capture and inspect network packets.
- Configure Snort and validate its configuration.
- Create and test a custom IDS rule.
- Generate and investigate security alerts.
- Analyze network traffic using PCAP files.

## Tools and Technologies

- **Snort:** Network intrusion detection and prevention.
- **Linux:** Command-line environment.
- **Terminal:** Configuration and command execution.
- **PCAP files:** Saved network traffic for analysis.
- **Virtual machine sandbox:** Controlled lab environment.

## Practical Exercises

### 1. Verify Snort Installation

```bash
snort -V
```

This command displays the installed Snort version.

### 2. Validate Snort Configuration

```bash
sudo snort -c /etc/snort/snort.conf -T
```

This checks whether the Snort configuration is valid.

### 3. Capture Network Traffic

```bash
sudo snort -v
```

Sniffer mode displays packet information.

Other useful options include:

- `-d`: Display packet payload data.
- `-e`: Display link-layer headers.
- `-X`: Display packet data in hexadecimal and ASCII.
- `-i`: Specify a network interface.

### 4. Log Network Packets

```bash
sudo snort -dev -K ASCII -l .
```

This captures and logs packet information in the current directory.

### 5. Run Snort in IDS Mode

Console alerts:

```bash
sudo snort -c /etc/snort/snort.conf -A console
```

Fast alert mode:

```bash
sudo snort -c /etc/snort/snort.conf -A fast
```

CMG alert mode:

```bash
sudo snort -c /etc/snort/snort.conf -A cmg
```

These modes provide different ways to view and investigate detected network activity.

## Creating a Custom IDS Rule

One of the most valuable exercises was creating a custom ICMP detection rule.

The rule used in the lab was:

```snort
alert icmp any any -> any any (msg: "ICMP Packet Found"; sid:1000001; rev:1;)
```

### Rule Breakdown

- `alert`: Generate an alert when the rule matches.
- `icmp`: Monitor ICMP traffic.
- `any any`: Match any source IP and source port.
- `->`: Specify traffic direction.
- `any any`: Match any destination IP and destination port.
- `msg`: Define the alert message.
- `sid`: Assign a unique rule identifier.
- `rev`: Specify the rule revision.

The rule was added to the local rules configuration and used to explore how custom detection logic generates alerts.

## Reviewing Security Alerts

I reviewed the Snort alert log using:

```bash
sudo cat /var/log/snort/alert
```

The lab produced ICMP-related alert entries, including the message:

```text
ICMP Packet Found
```

The alert output included timestamps, rule identifiers, protocol information and source and destination IP addresses.

**Investigation note:** The captured alert output identified IPv6-ICMP traffic, while the custom rule above uses Snort's `icmp` protocol keyword. This is worth verifying against the loaded rules and Snort version before attributing those specific alerts to that rule.

## PCAP Analysis

I also explored analyzing saved packet captures.

Read a PCAP file:

```bash
snort -r icmp-test.pcap
```

Run Snort with IDS configuration against a PCAP:

```bash
sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10
```

This helped me understand how previously captured network traffic can be reviewed for suspicious activity.

## Key Learnings

Through this lab, I gained practical experience with:

- Network packet inspection and logging.
- Snort configuration and operating modes.
- IDS alert generation.
- Custom Snort rule structure.
- ICMP traffic monitoring.
- Reviewing alert logs.
- PCAP-based traffic investigation.

The main lesson I took away is that **generating an alert is only the beginning of an investigation**. A SOC Analyst must examine the available evidence and determine whether the activity is legitimate or suspicious.


## Conclusion

This project strengthened my understanding of network security monitoring and intrusion detection through practical exercises with Snort.

My next learning objectives are to develop more advanced detection rules, investigate suspicious traffic patterns and explore Snort's inline IPS capabilities.

**Learn. Practice. Investigate. Document. Improve.**

---

*This lab was completed in a controlled virtual machine sandbox for educational purposes.*

*Author: Aspiring SOC Analyst*

*Project focus: Cybersecurity | Network Security | Snort | IDS | SOC Operations* 
# Related Article

Read my detailed lab walkthrough on Medium:https://medium.com/@boshhirad/snort-lab-project-hands-on-network-monitoring-intrusion-detection-and-custom-ids-rules-d301cc6178a5?postPublishedType=repub 

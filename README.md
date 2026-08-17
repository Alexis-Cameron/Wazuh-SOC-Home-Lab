# Wazuh SOC Home Lab

A hands-on SOC home lab demonstrating endpoint monitoring, security event detection, brute-force attack simulation, and incident containment using Wazuh, Ubuntu, Fail2ban, and UFW.

## Project Overview

This project was built to simulate a small Security Operations Center (SOC) environment using an Ubuntu virtual machine monitored by Wazuh.

The lab demonstrates the complete workflow of:

- Generating security events
- Detecting authentication failures
- Creating a custom brute-force detection rule
- Generating a Level 12 security alert
- Investigating events in the Wazuh dashboard
- Using Fail2ban for SSH protection
- Using UFW to demonstrate firewall-based containment

## Lab Environment

- Host OS: Windows
- Virtualization: VirtualBox
- Endpoint: Ubuntu 24.04 LTS
- SIEM/XDR: Wazuh
- Intrusion Prevention: Fail2ban
- Firewall: UFW
- SSH: OpenSSH

## Wazuh Components

The Wazuh environment was installed and configured with:

- Wazuh Indexer
- Wazuh Manager
- Wazuh Filebeat
- Wazuh Dashboard

The Wazuh agent monitored the Ubuntu endpoint and forwarded security events for analysis.

## Security Monitoring & Detection

### Authentication Failure

Failed login attempts were generated on the Ubuntu endpoint and successfully detected by Wazuh.

Wazuh identified the event as:

`PAM: User login failed.`

The event was investigated through the Wazuh dashboard.

### Custom Brute-Force Detection

A custom Wazuh rule was created to identify simulated brute-force activity.

The rule generated a **Level 12 alert** when the simulated brute-force event was detected.

### Password Guessing Detection

Authentication failures were investigated through Wazuh Threat Hunting to demonstrate how an analyst could identify password-guessing activity.

## Incident Containment

### Fail2ban

Fail2ban was installed and configured to monitor SSH authentication activity.

The SSH jail was verified through the Fail2ban client.

### UFW Firewall

UFW was configured to allow required services while demonstrating IP-based firewall containment.

A test IP address was temporarily denied and the firewall rules were verified before the rule was removed.

## Attack Simulation

The lab simulated several security events:

1. Failed authentication attempts
2. Password-guessing activity
3. A custom Level 12 brute-force detection event

These events were then investigated through the Wazuh dashboard.

## Evidence

Screenshots documenting the lab are available in the `screenshots` directory.

The evidence includes:

- Custom Wazuh brute-force rule
- Fail2ban configuration/status
- UFW firewall containment
- Wazuh dashboard overview
- Authentication failure details
- Level 12 brute-force alert
- Password-guessing investigation

## Key Takeaways

This lab provided hands-on experience with:

- SIEM monitoring
- Linux security logs
- Authentication event analysis
- Detection rule creation
- Brute-force detection
- Security alert investigation
- SSH protection with Fail2ban
- Firewall-based incident containment
- Security event investigation using Wazuh

## Project Structure

```text
Wazuh-SOC-Home-Lab/
│
├── README.md
│
├── commands/
│   └── lab-commands.md
│
└── screenshots/
    ├── Custom_Brute_Force_Rule_Added.png
    ├── Fail2ban_Status.png
    ├── UFW_Firewall_Containment_Level12.png
    ├── Wazuh_Dashboard_Overview.png
    ├── Wazuh_Failed_Login_Details.png
    ├── Wazuh_Level12_Brute_Force_Alert.png
    └── Wazuh_Threat_Hunting_Password_Guessing.png

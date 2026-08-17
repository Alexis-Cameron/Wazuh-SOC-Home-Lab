# Wazuh SOC Home Lab — Commands

## 1. System Preparation

The Ubuntu VM was created, updated and the required security tools were installed.

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y curl wget git ufw fail2ban
```

## 2. Configure SSH

SSH was enabled and configured to use port 600 for the lab.

```bash
sudo systemctl enable --now ssh
sudo ufw allow 600/tcp
```

## 3. Configure UFW Firewall

UFW was enabled and configured to allow the required SSH and HTTPS services.

```bash
sudo ufw allow 600/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status
```

## 4. Install Fail2ban

Fail2ban was installed and enabled to provide SSH brute-force protection.

```bash
sudo apt install -y fail2ban
sudo systemctl enable --now fail2ban
```

## 5. Verify Fail2ban

The Fail2ban service and SSH jail were verified.

```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

## 6. Install Wazuh

The Wazuh installation assistant was downloaded and used to install the Wazuh components.

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

## 7. Start Wazuh Services

The Wazuh Dashboard, Indexer, and Manager services were started.

```bash
sudo systemctl start wazuh-dashboard wazuh-indexer wazuh-manager
```

## 8. Verify Wazuh Services

The Wazuh services were checked to confirm they were running.

```bash
sudo systemctl status wazuh-dashboard wazuh-indexer wazuh-manager
```

## 9. Create Custom Brute-Force Detection Rule

The Wazuh local rules file was edited to create a custom Level 12 brute-force detection rule.

```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```

The following rule was added:

```xml
<group name="local,syslog,sshd,authentication_failed,attack,brute_force,">

  <rule id="100002" level="12">
    <match>SOC_SIMULATED_BRUTE_FORCE</match>
    <description>Simulated brute force attack detected</description>
    <group>authentication_failed,attack_brute_force,</group>
  </rule>

</group>
```

## 10. Restart Wazuh Manager

The Wazuh Manager was restarted so the custom rule could be loaded.

```bash
sudo systemctl restart wazuh-manager
```

## 11. Generate Simulated Brute-Force Event

A simulated brute-force event was generated using the Linux logging system.

```bash
logger "SOC_SIMULATED_BRUTE_FORCE"
```

The event was then investigated in the Wazuh Dashboard and generated a Level 12 alert.

## 12. Generate Authentication Failure Events

Failed authentication attempts were intentionally generated on the Ubuntu VM.

These events were collected by Wazuh and appeared as authentication failure alerts in the dashboard.

## 13. Test UFW Firewall Containment

A test IP address was temporarily blocked to demonstrate firewall-based containment.

```bash
sudo ufw deny from 192.0.2.100
sudo ufw status numbered
```

## 14. Remove Firewall Containment Rule

The temporary test rule was removed after verifying the firewall configuration.

```bash
sudo ufw delete deny from 192.0.2.100
sudo ufw status numbered
```

## 15. Verify Fail2ban Configuration

Fail2ban was checked again to confirm the SSH jail was active.

```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

## 16. Lab Outcome

The completed lab demonstrated:

- Ubuntu endpoint monitoring
- Wazuh SIEM deployment
- Authentication failure detection
- Custom Level 12 brute-force detection
- Password-guessing investigation
- Fail2ban SSH protection
- UFW firewall containment
- Security event investigation through the Wazuh Dashboard

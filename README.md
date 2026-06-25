# Home-soc-lab

## Overview
A home Security Operations Center (SOC) lab built to 
simulate real-world cyberattacks and practice defensive 
security skills. The lab uses Wazuh as a SIEM to monitor 
a victim machine, detect attacks in real time, and 
generate alerts mapped to the MITRE ATT&CK framework. 
Incidents are documented through formal incident response 
reports to simulate real SOC analyst workflows.

## Lab Architecture
- **SIEM Server:** Wazuh v4.14.5 (VirtualBox VM)
- **Victim Machine:** Ubuntu Server 22.04 (VirtualBox VM)  
- **Attacker Machine:** Kali Linux (physical machine)

## Tools Used
- Wazuh SIEM
- Kali Linux
- Hydra
- Nmap
- VirtualBox

## Attacks Simulated
| Attack | Tool | MITRE Technique | Report |
|--------|------|----------------|--------|
| SSH Brute Force | Hydra | T1110.001 | [IR-001](reports/IR-001-SSH-Brute-Force.md) |
| Nmap Reconnaissance | Nmap | T1046 | [IR-002](reports/IR-002-Nmap-Scan.md) |
| Privilege Escalation | GTFOBins (sudo find) |T1548.003 | [IR-003](reports/IR-003-Privilege-Escalation.md) |
| Persistence | useradd | T1136.001 + T1078.003 | [IR-004](reports/IR-004-Persistence.md) |
## Custom Detection Rules
| Rule ID | Description | Detects |
|---------|-------------|---------|
| 100002 | Nmap scan detection | T1046 |

## Status
In Progress — more attacks being added

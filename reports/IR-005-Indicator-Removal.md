INCIDENT RESPONSE REPORT 005
Date: 09/07/2026 
Severity: High
Status: Open (system retained in current state for continued lab testing)

Summary: Wazuh detected suspicious activity on ubuntu-victim (192.168.1.27). The attacker, after gaining initial access via SSH as backdoor account netmon1, then used the compromised victim account to clear the contents of /var/log/auth.log to remove evidence of their activity. This was detected by Wazuh's FIM (File Integrity Monitoring) via syscheck, which triggered Rule 592 when the log file size was reduced to zero. Additionally, the attacker cleared their .bash_history file to remove command history, which went undetected representing a detection gap. Notably, Wazuh misclassified the alert as T1565.001 (Stored Data Manipulation) instead of T1070 (Indicator Removal), highlighting a limitation in Wazuh's default MITRE mapping.

Timeline:
Jul 9, 2026 @ 11:11:27.862  ubuntu-victim sshd: authentication success. 3 5715
Jul 9, 2026 @ 11:12:14.367 ubuntu-victim Log file size reduced. 8 592
Evidence:
Attacker IP: 192.168.1.12
Victim IP: 192.168.1.27
Accounts used: netmon1, victim
Rule id: 592, 5715
Rule Description: Log  File size reduced, sshd authentication success

MITRE ATT&CK:
Wazuh detected: T1565.001  Stored Data Manipulation (misclassification) 
Correct technique: T1070.003  Clear Command History, T1070.004  File Deletion 
Tactic: Defense Evasion
 
Conclusion: This attack demonstrates a critical detection gap, the attacker successfully cleared /var/log/auth.log, blinding Wazuh's ability to monitor future authentication events. The .bash_history file was also cleared with no alert generated. Additionally, Wazuh's default MITRE mapping misclassified the action as Impact rather than Defense Evasion.

Recommended Actions:
1)	Re-enable logging: sudo systemctl restart rsyslog to regenerate auth.log 
2)	Enable FIM on .bash_history for all users to close the detection gap 
3)	Review and update Wazuh's default MITRE mappings for log clearing events 
4)	Delete backdoor account netmon1: sudo userdel -r netmon1 
5)	Block source IP 192.168.1.12 at the firewall 
6)	Note: Remediation deferred: system retained for continued lab testing
 



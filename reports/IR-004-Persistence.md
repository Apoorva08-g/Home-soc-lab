INCIDENT RESPONSE REPORT 004
Date: 21/06/2026 
Severity: High
Status: Open (system retained in current state for continued lab testing)



Summary: Wazuh detected a new user and group addition with name netmon1, later after the machine was rebooted it also detected login as the same new user created with ssh from the suspicious ip 192.168.1.12.

Timeline:
Jun 21, 2026 @ 00:00:43.889 ubuntu-victim New user added to the system.  8  5902
Jun 21, 2026 @ 00:00:43.886 ubuntu-victim New group added to the system.  8  5901
Jun 21, 2026 @ 00:00:56 ubuntu-victim system rebooted
Jun 21, 2026 @ 00:19:46.675 ubuntu-victim sshd: authentication success.       3 5715

Evidence:
Attacker IP: 192.168.1.12
Victim IP: 192.168.1.27
New User: netmon1
Rule id: 5901, 5902, 5715
Rule Description: New Group added to  system, New user added to system, Sshd: authentication success
MITRE ATT&CK:
rule.mitre.id: T1136.001, T1078.003
rule.mitre.technique: Create Account, Valid Accounts

Conclusion: This is a critical security breach with the attacker trying to create  backdoor.

Recommended Actions:
(1)	Remove the account netmon1 (sudo userdel -r netmon1) 
(2)	Audit the system to look for any permissions modified or passwords compromised.
(3)	Check System logs to see the activity
(4)	Block the ip address to stop any further actions

 

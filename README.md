# RedKross_01
MITRE ATT&amp;CK_C0014<BR>
Author Bhoomi Sanjay Wadke
# Operation Wocao — Campaign Research Report

**MITRE ATT&CK Campaign ID:** C0014
**Intern ID:** 2114
**Researched & Documented By:** Bhoomi Sanjay Wadke
**Submission Date:** 15 May 2026

---

## Overview

This repository contains a comprehensive research report on **Operation Wocao**, a large-scale cyber espionage campaign (MITRE ATT&CK Campaign ID: C0014) active from December 2017 to December 2019. The report also includes detailed documentation of MITRE ATT&CK Software entries **S0140 through S0150**.

---

## Document Structure

### Part 1 — Operation Wocao Campaign Report (C0014)

| Section | Title |
|---------|-------|
| 1 | Campaign Overview |
| 2 | Threat Actor / Group Association |
| 3 | Timeline |
| 4 | Objectives of Attack |
| 5 | Targeted Sectors & Countries |
| 6 | Attack Flow |
| 7 | MITRE ATT&CK Techniques Used |
| 8 | Real-World Incidents |
| 9 | Detection Opportunities |
| 10 | Defensive Recommendations |
| 11 | Indicators of Compromise (IOCs) |
| 12 | Tools and Malware Used |
| 13 | Research Analysis |
| 14 | References |
| 15 | Conclusion |

### Part 2 — MITRE ATT&CK Software Research (S0140–S0150)

| Software ID | Name | Type | Threat Actor |
|-------------|------|------|--------------|
| S0140 | Shamoon (Disttrack) | Wiper Malware | Cutting Sword of Justice / APT33 |
| S0141 | Winnti for Windows | RAT | Winnti Group / Aquatic Panda |
| S0142 | StreamEx | Malware | Deep Panda |
| S0143 | Flame (Flamer/sKyWIper) | Espionage Toolkit | Nation-State (suspected Israel/USA) |
| S0144 | ChChes (Scorpion/HAYMAKER) | Trojan | menuPass / APT10 |
| S0145 | POWERSOURCE (DNSMessenger) | PowerShell Backdoor | FIN7 |
| S0146 | TEXTMATE | Memory-Resident Backdoor | FIN7 |
| S0147 | Pteranodon (Pterodo) | Surveillance Backdoor | Gamaredon Group |
| S0148 | RTM (Redaman) | Banking Malware | RTM Group |
| S0149 | MoonWind | RAT | Unidentified China-linked Actor |
| S0150 | POSHSPY | PowerShell Backdoor | APT29 / Cozy Bear |

---

## Campaign Quick Facts — Operation Wocao

| Attribute | Details |
|-----------|---------|
| Campaign Type | Advanced Cyber Espionage |
| Duration | December 2017 — December 2019 (2 Years) |
| Attributed To | Suspected China-Based Threat Actors (APT20 Overlap) |
| Countries Targeted | Brazil, China, France, Germany, Italy, Mexico, Portugal, Spain, UK, USA |
| Sectors Targeted | Government, Aviation, Energy, Finance, Healthcare, Transportation, Software, Insurance, Offshore Engineering, Construction |
| Scale | 10+ Countries, 10+ Sectors |
| ATT&CK Techniques | 60+ MITRE ATT&CK Techniques |
| Primary Goal | Credential Theft, Data Exfiltration, Persistent Access |
| MITRE ATT&CK ID | C0014 |

---

## Attack Flow Summary

```
Initial Access
    ↓
JBoss Exploitation (T1190) / VPN with Stolen Credentials (T1133/T1078)
    ↓
Execution
    ↓
Webshell + PowerShell / CMD / Python Backdoors (T1059.001/003/006)
    ↓
Persistence
    ↓
Scheduled Tasks (T1053.005) + Service Creation (T1569.002)
    ↓
Defense Evasion
    ↓
Log Clearing + File Deletion + Masquerading + Obfuscation (T1070/T1036)
    ↓
Credential Access
    ↓
Mimikatz DCSync + LSASS Dump + Kerberoasting + MFA Interception
    ↓
Discovery
    ↓
Network Scanning + Active Directory Enumeration (BloodHound, dsquery)
    ↓
Lateral Movement
    ↓
SMB / PsExec / Impacket smbexec.py (T1021.002 / T1570)
    ↓
Collection
    ↓
Clipboard + Keylogging + File Archiving with WinRAR
    ↓
Exfiltration
    ↓
XServer Backdoor over C2 via Tor Exit Nodes (T1041 / T1090.003)
```

---

## Key MITRE ATT&CK Techniques

| Technique ID | Technique Name | Purpose |
|---|---|---|
| T1190 | Exploit Public-Facing Application | Initial access via JBoss |
| T1078 | Valid Accounts | Unauthorized VPN login |
| T1003.001 | OS Credential Dumping: LSASS Memory | Credential theft |
| T1047 | Windows Management Instrumentation | Remote execution |
| T1059.001 | PowerShell | Command execution |
| T1558.003 | Kerberoasting | Password cracking |
| T1041 | Exfiltration Over C2 Channel | Data theft |
| T1090.003 | Proxy: Multi-hop Proxy (Tor) | Anonymized C2 |
| T1027.010 | Command Obfuscation | Defense evasion |
| T1071.001 | Web Protocols | C2 communication |

---

## Tools & Malware Used

| Tool | Purpose |
|------|---------|
| Mimikatz | Credential dumping |
| BloodHound | Active Directory reconnaissance |
| Impacket | Lateral movement |
| PsExec | Remote execution |
| PowerSploit | Kerberoasting |
| Tor | Anonymous C2 communication |
| Wevtutil | Windows event log deletion |
| netstat | Network discovery |
| dsquery | Active Directory enumeration |
| XServer Backdoor | Custom C2 backdoor |

---

## Key Takeaways

1. **MSP Targeting is a force-multiplier** — compromising one managed service provider can lead to dozens of downstream victims.
2. **MFA alone is insufficient** — Operation Wocao actors demonstrated soft token interception capability.
3. **Credential hygiene is critical** — stolen VPN credentials were a primary initial access vector.
4. **Centralized logging is essential** — actors cleared local Windows Event Logs using Wevtutil to destroy forensic evidence.
5. **Tools are actively modified** — actors customized open-source tools to evade signature-based detection.
6. **Low-and-slow intrusions are hard to detect** — the campaign persisted undetected for nearly 2 years.

---

## Defensive Recommendations

- Enable **MFA** for all VPNs, admin accounts, and remote access systems
- Apply **continuous patch management** for public-facing applications
- Deploy **EDR solutions** for behavioral detection
- Implement **network segmentation** between sensitive and general systems
- Enforce **principle of least privilege** for all accounts
- Enable centralized **log monitoring** (SIEM) to prevent local log tampering
- Regularly scan web servers for **webshells**
- Conduct **threat hunting** using MITRE ATT&CK mappings

---

## Common Indicators of Compromise (IOCs)

- Suspicious PowerShell execution with Base64/XOR encoding
- Unauthorized VPN logins from unusual geolocations
- Webshell files present on web servers
- Unusual ports in use: **25667**, **47000**
- Abnormal WMI and PsExec usage
- Windows Event Log deletion activity (Wevtutil)
- Unexpected outbound encrypted traffic through Tor exit nodes

---

## References

- [MITRE ATT&CK — Operation Wocao (C0014)](https://attack.mitre.org/campaigns/C0014)
- Fox-IT Report: *"Operation Wocao: Shining a light on one of China's hidden hacking groups"* — Maarten van Dantzig & Erik Schamper (December 19, 2019)
- [MITRE ATT&CK Software S0140–S0150](https://attack.mitre.org/software/)

---

## About This Report

This research was conducted as part of an internship assignment covering MITRE ATT&CK Campaign C0014 and Software range S0140–S0150. Each software entry includes full ATT&CK technique mappings, execution methods, persistence techniques, IOCs, detection opportunities, and mitigation strategies.

> **Intern ID:** 2114 | **Campaign:** C0014 — Operation Wocao | **Software Range:** S0140–S0150

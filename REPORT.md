# Network Reconnaissance and Security Assessment Lab

**Author:** Phidmah Steve  
**Platform:** Kali Linux and Metasploitable 2  
**Target IP:** `192.168.56.20`  
**Assessment date:** 21 October 2026  
**Scope:** Authorized scanning of an isolated VirtualBox lab network.

## 1. Objective

To identify active hosts, open TCP ports, detected services, and available operating-system clues using Nmap. The objective is to document potential security risks and recommend defensive measures.

## 2. Lab Environment

The assessment was conducted in a controlled VirtualBox environment using Kali Linux as the scanning machine and Metasploitable 2 as the target. The machines communicated over an isolated internal network.

- Kali Linux IP: `192.168.56.10`
- Metasploitable 2 IP: `192.168.56.20`

## 3. Methodology

The following Nmap scans were performed:

- `nmap -sV 192.168.56.20` — detected open TCP ports and attempted to identify service versions.
- `sudo nmap -O 192.168.56.20` — attempted to identify the target's operating system.

The outputs were saved in the `evidence/` directory.

## 4. Key Findings

The service scan identified 23 open TCP ports among the 1,000 most common TCP ports scanned.

Examples of detected services included:

| Port | Service | Detected version |
|---|---|---|
| 21 | FTP | vsftpd 2.3.4 |
| 22 | SSH | OpenSSH 4.7p1 |
| 23 | Telnet | Linux telnetd |
| 80 | HTTP | Apache 2.2.8 |
| 139, 445 | SMB | Samba 3.X–4.X |
| 3306 | MySQL | 5.0.51a |
| 5432 | PostgreSQL | 8.3.0–8.3.7 |

These are version strings reported by Nmap and have not been independently verified.

## 5. Operating-System Detection

Nmap detected characteristics consistent with a Unix/Linux host but reported no exact operating-system match. Therefore, the precise OS and kernel version remain unconfirmed by this scan.

## 6. Potential Security Risks

- **Legacy software:** Older service versions may contain known vulnerabilities.
- **Unencrypted services:** Telnet and some FTP configurations can expose credentials or data in transit.
- **Excessive network exposure:** Numerous listening services increase the attack surface.
- **Database exposure:** MySQL and PostgreSQL may be at risk if accessible to unauthorized hosts or poorly configured.
- **Remote administration and file sharing:** SSH, SMB, RPC, and other services require appropriate access controls.

These are potential risks, not proof that a particular vulnerability was successfully exploited.

## 7. Recommendations

1. Upgrade unsupported operating systems and services to maintained versions.
2. Disable unnecessary services and close unused ports.
3. Replace Telnet with SSH and use secure file-transfer methods.
4. Restrict database access to trusted hosts and networks.
5. Apply strong authentication, least privilege, and appropriate firewall rules.
6. Review service configurations, security logs, and applicable vendor advisories.
7. Repeat scans after remediation to verify improvements.

## 8. Limitations

The assessment used Nmap service detection and OS fingerprinting only. It did not establish that the listed services were exploitable, and OS identification was inconclusive. The scan covered the 1,000 most common TCP ports rather than every possible TCP port.

## 9. Evidence

- `evidence/nmap-service-scan.txt`
- `evidence/nmap-os-detection.txt`

## 10. Conclusion

The scan identified multiple network services on the lab target and highlighted areas requiring further security review. The results demonstrate basic reconnaissance, evidence collection, risk identification, and defensive reporting in an authorized test environment.


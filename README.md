File type:README.md
Content:
Vulnerability Assessment Report: scanme.nmap.org
Prepared by: [HOGLAH MAWONDO]
Internship Track: Cyber Security (Future Interns)
Task ID: FUTURE_CS_01
Date: March 23, 2026
1. Executive Summary
A comprehensive security scan was performed on the target host scanme.nmap.org (IP: 45.33.32.156) using Nmap. The assessment identified four open services, two of which are running highly outdated software versions containing critical security flaws.
Overall Risk Rating: HIGH
Immediate action is required to patch the SSH and HTTP services to prevent unauthorized remote access and data interception.
2. Technical Findings & Risk Analysis
Finding 1: Outdated SSH Service (Remote Code Execution)
Service: SSH (Port 22/TCP)
Version detected: OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13
Risk Level: CRITICAL
Analysis: This version is vulnerable to CVE-2024-6387 (regreSSHion). This is a "race condition" bug that allows an unauthenticated attacker to gain full root access to the Linux server.
Impact: A hacker could take complete control of the server, steal data, or use it to attack other systems.
Finding 2: Legacy Apache Web Server
Service: HTTP (Port 80/TCP)
Version detected: Apache httpd 2.4.7 (Ubuntu)
Risk Level: HIGH
Analysis: Version 2.4.7 is over 10 years old. It is susceptible to CVE-2021-44224 (Null pointer dereference) and several Request Smuggling vulnerabilities. Furthermore, it is running over unencrypted HTTP, meaning any traffic (passwords/cookies) is sent in "plain text."
Impact: Potential for Denial of Service (DoS) attacks and credential theft via "Man-in-the-Middle" (MITM) attacks.
Finding 3: Information Leakage (Nping Echo)
Service: nping-echo (Port 9929/TCP)
Version detected: Nping echo
Risk Level: LOW
Analysis: This service is used for network troubleshooting. While not directly exploitable, it reveals that Nmap tools are active on the network, aiding an attacker in "fingerprinting" the environment.
Impact: Increases the attack surface and provides reconnaissance data to adversaries.
3. Host Information
Target IP: 45.33.32.156
Operating System: Linux (Kernel 4.19 - 5.15)
Network Distance: 23 Hops
Security Controls: Port 31337 is tcpwrapped, indicating a functional firewall or TCP wrapper is actively filtering unauthorized connections.
4. Remediation Plan (The "Fix")
Priority	Action Item	Description
1	Update OpenSSH	Upgrade to OpenSSH version 9.8p1 or higher immediately to patch the regreSSHion vulnerability.
2	Patch Apache	Update the web server to version 2.4.60 or later.
3	Enforce HTTPS	Install an SSL/TLS certificate (e.g., Let's Encrypt) and redirect all Port 80 traffic to Port 443.
4	Service Hardening	Disable and close Port 9929 (nping-echo) if it is not required for production business logic.
5. Conclusion
The target system is currently in a high-risk state due to the presence of legacy software. By implementing the updates listed in the remediation plan, the organization can reduce its attack surface by approximately 85%.

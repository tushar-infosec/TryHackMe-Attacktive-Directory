# TryHackMe – Attacktive Directory  
## Active Directory Domain Compromise Writeup  

---

## Medium Blog  
https://medium.com/@tusharmumbre/tryhackme-active-directory-walkthrough-full-domain-compromise-e02bb6217008  

---

## 1. Introduction  

This repository presents a detailed penetration testing walkthrough of the **Attacktive Directory** lab from TryHackMe.  

The objective of this exercise was to simulate a real-world internal network attack against an Active Directory environment and achieve full domain compromise starting without any initial credentials.  

---

## 2. Target Information  

**Target IP Address:** 10.49.166.19  
**Domain Name:** spookysec.local  
**Operating System:** Windows Server 2019  
**Environment:** Active Directory Domain Controller  

---

## 3. Methodology  

The assessment was conducted following a structured penetration testing approach:  

- Reconnaissance  
- Enumeration  
- Exploitation  
- Post-Exploitation  
- Privilege Escalation  

---

## 4. Attack Overview  

The compromise was achieved through a sequence of misconfigurations and weak security controls within the Active Directory environment.  

**Attack Chain:**  
ASREPRoasting → Password Cracking → SMB Enumeration → Credential Discovery → DCSync Attack → Pass-the-Hash  

---

## 5. Detailed Execution  

### 5.1 Reconnaissance  
An Nmap scan was performed to identify open ports and services. The presence of Kerberos, LDAP, and SMB confirmed that the target system was functioning as a Domain Controller.  

### 5.2 Enumeration  
SMB enumeration and Kerberos-based user enumeration were conducted using enum4linux and Kerbrute. This resulted in the identification of multiple valid domain users, including a service account.  

### 5.3 Exploitation  
The service account (**svc-admin**) was found vulnerable to ASREPRoasting due to disabled pre-authentication. A Kerberos hash was extracted and successfully cracked using Hashcat.  

### 5.4 Post-Exploitation  
Using the obtained credentials, SMB shares were accessed. A backup share contained encoded credentials, which were decoded to reveal valid domain credentials.  

### 5.5 Privilege Escalation  
The backup account had replication privileges, enabling a DCSync attack. This allowed extraction of NTLM password hashes for all domain users.  

### 5.6 Domain Compromise  
Using the Administrator hash, Pass-the-Hash authentication was performed via Evil-WinRM, resulting in full Domain Admin access.  

---

## 6. Tools Utilized  

- Nmap  
- Enum4linux  
- Kerbrute  
- Impacket Toolkit  
- Hashcat  
- SMBClient  
- Evil-WinRM  

---

## 7. Key Findings  

- Kerberos pre-authentication was disabled for a service account  
- Weak password policy enabled instant hash cracking  
- Sensitive credentials were stored in an accessible SMB share  
- Excessive privileges were assigned to the backup account  

---

## 8. Security Recommendations  

- Enforce strong password policies across all accounts  
- Enable Kerberos pre-authentication for all users  
- Restrict and audit SMB share access  
- Limit replication privileges strictly to Domain Controllers  
- Monitor for abnormal Kerberos and replication activity  

---

## 9. Conclusion  

This lab demonstrates how multiple small misconfigurations in an Active Directory environment can be chained together to achieve full domain compromise.  

It highlights the importance of secure configurations, proper privilege management, and continuous monitoring in enterprise environments.  

---

## 10. Detailed Report  

The complete penetration testing report is available below:  

- [Download Full Report](Attacktive_Directory_Writeup.docx)  

This document contains full commands, outputs, and step-by-step execution details.  

---

## 11. Purpose  

This project is part of my cybersecurity learning journey and demonstrates practical knowledge of Active Directory attacks, penetration testing methodology, and post-exploitation techniques.  

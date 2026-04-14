TryHackMe - Attacktive Directory Writeup

Medium Blog:
https://medium.com/@tusharmumbre/tryhackme-active-directory-walkthrough-full-domain-compromise-e02bb6217008


Overview

This repository contains my complete walkthrough and analysis of the "Attacktive Directory" room on TryHackMe. 

The objective of this lab was to perform a full Active Directory domain compromise starting without any credentials and ending with Administrator-level access.

Target Details:
- IP Address: 10.49.166.19
- Domain: spookysec.local
- Operating System: Windows Server 2019


Attack Summary

The attack followed a structured penetration testing approach:

1. Reconnaissance
Performed an Nmap scan to identify open ports and services. This confirmed that the target was a Domain Controller.

2. Enumeration
Used tools like enum4linux and Kerbrute to gather domain information and identify valid usernames.

3. Exploitation
Performed ASREPRoasting on a vulnerable account (svc-admin) to obtain a Kerberos hash, which was then cracked using Hashcat.

4. Post-Exploitation
Used the cracked credentials to access SMB shares and discovered backup credentials stored in a file.

5. Privilege Escalation
Executed a DCSync attack using the backup account to dump all domain password hashes.

6. Final Access
Used Pass-the-Hash technique to gain Administrator access to the system.


Tools Used

- Nmap
- Enum4linux
- Kerbrute
- Impacket
- Hashcat
- SMBClient
- Evil-WinRM


Key Learnings

This lab demonstrated how small misconfigurations in Active Directory can lead to full domain compromise. 

Some important lessons:
- Weak passwords can be cracked very quickly
- Kerberos misconfigurations (like disabled pre-authentication) are dangerous
- Sensitive credentials should never be stored in shared folders
- DCSync attacks can expose the entire domain


Full Report

The complete detailed report is available in this repository as a document file. It includes all commands, outputs, and step-by-step explanations.


Purpose

This project is part of my cybersecurity learning journey and is intended to demonstrate my understanding of Active Directory attacks and penetration testing methodology.

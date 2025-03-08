---
layout: default
title: "Whitehatters Computer Security Club (WCSC) Notes"
---

# 🏴‍☠️ Whitehatters Computer Security Club (WCSC) Notes

This page contains my notes from WCSC meetings at USF.

## 📌 Meeting Notes
# Red Teaming & Networking Basics

## Web Penetration Testing (2/7/24)
- Majority of Red Teaming involves web penetration testing.
- Two types: **Web Application Penetration Testing** and **Bug Bounty**.
- **Important Concepts**:
  - **Enumeration**: Fully enumerate all areas.
  - **Note-Taking**: Essential in web exploitation.
  - **Website Code**: HTML, CSS, JavaScript.
  - **Client-Side**: User interface interaction, only affects client.
  - **Server-Side**: Data storage, sensitive data management.
  - **PHP**: Common in e-commerce.
  - **SQL**: Used for database storage.
  - **Data Formats**: JSON, XML, CSV.
  - **HTTP Codes**:
    - 1xx: Informational
    - 2xx: Successful
    - 3xx: Redirection
    - 4xx: Client Errors
    - 5xx: Server Errors
  - **Protocols**: HTTP vs HTTPS, URL structure.
  - **Useful Tools**:
    - Robots.txt, Sitemap.xml, and source code analysis.
  
### Next Week: Exploitation

## Networking Basics (2/12/24)
- **OSI Model**: Seven layers from Physical to Application.
  - **Physical (Layer 1)**: Cables, transmission of binary data via electricity or light.
  - **Data Link (Layer 2)**: LAN, MAC addresses, ARP, and MAC flooding.
  - **Network (Layer 3)**: IP addresses, routing, Man-in-the-Middle attacks.
  - **Transport (Layer 4)**: TCP vs UDP.
  - **Session (Layer 5)**: Establishes and manages connections.
  - **Presentation (Layer 6)**: Data formatting, phishing.
  - **Application (Layer 7)**: User interface, where attacks occur.
  
### Subnetting
- **Subnet Mask**: Splits IP address into network and host parts.
- **Common Protocols**:
  - **DHCP**: Dynamically assigns IP addresses.
  - **FTP**: Transfers files.
  - **SSH**: Secure remote connections.
  - **SMTP, POP3, IMAP**: Email protocols.

## Advanced Web Exploitation (2/14/24)
- **Burp Suite**: Key tool for web exploitation.
- **Authentication**: Bypassing authentication processes.

## Capture the Flag (2/19/24 & 9/23/24)
- **Steganography Tools**:
  - Stegseek, binwalk, strings, AperiSolve.
- **Cryptography**:
  - Caesar Cipher, Vigenère Cipher, Hashing, Public Key.

## OSINT (10/30/24)
- **OS-Based Tools**:
  - SS64, ExplainShell, Man Pages.
- **Miscellaneous**:
  - Any.Run (live sandbox tool), URLScan, TimeStampConverter, AADInternals.
- **Network-Based Tools**:
  - VirusTotal, AbuseIPDB, MX Toolbox, ThreatFox IOC Database.
- **Tool Highlights**:
  - **VirusTotal**: Used in 95% of alerts.
  - **HybridAnalysis**: File and URL sandboxing.

---
layout: default
title: "HTB Notes"
---

# 🏆 HTB Notes

This page contains my notes on Hack The Box (HTB) Academy. 

# Connecting Using VPN
- When connected to a VPN, data originates from the VPN server rather than our computer and will appear to originate from a public IP address other than our own.
- When connecting to a VPN (either within HTB Academy or the main HTB platform), we connect using the following command:

    ```bash
    sudo openvpn user.ovpn
    ```
- The last line `Initialization Sequence Completed` tells us that we successfully connected to the VPN.
- The `user.ovpn` file is the VPN key that we download from either the Academy module section or the main HTB platform Access page.
- If we type `ifconfig` in another terminal window, we will see a `tun` adapter if we successfully connected to the VPN.
- Typing `netstat -rn` will show us the networks accessible via the VPN.
---
# Basic Tools
- **Netcat** comes pre-installed in most Linux distributions. We can also download a copy for Windows machines from this link. There's another Windows alternative to netcat coded in PowerShell called **PowerCat**. Netcat can also be used to transfer files between machines, as we'll discuss later.
- **Terminal multiplexers**, like `tmux` or `Screen`, are great utilities for expanding a standard Linux terminal's features, like having multiple windows within one terminal and jumping between them. Let's see some examples of using `tmux`, which is the more common of the two.

    - If `tmux` is not present on our Linux system, we can install it with the following command:
    ```bash
    sudo apt install tmux -y
    ```
---
# Service Scanning

(Placeholder for content related to service scanning.)
---
# Privilege Escalation
- There may be ssh keys we can read in `/root/.ssh/id_rsa`
- We can use that key and copy it to gain access to root. Example:
    ```bash
    ssh root@83.136.251.146 -i rsa_id -p 37279
    ```
---
# Transferring Files
- For example, if we wanted to transfer a binary file called `shell`, we can base64 encode it as follows:
    ```bash
    base64 shell -w 0
    ```
- Now, we can copy this base64 string, go to the remote host, and use `base64 -d` to decode it, and pipe the output into a file:
    ```bash
    echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > shell
    ```
- To validate the format of a file, we can run the `file` command on it:
    ```bash
    file shell
    ```
---
# Starting Out
## Resources
### YouTube Channels
(Placeholder for YouTube channel links related to HTB or other resources.)
### Blogs
One great blog worth checking out is [0xdf hacks stuff](https://0xdf.hackstuff.io). This blog has fantastic walkthroughs of most retired HTB boxes, each with a "Beyond Root" section covering some unique aspect of the box that the author noticed.
---
# Common Pitfalls
- In case we start facing some issues with connecting to SSH servers or connecting to our machine from a remote server, we may want to renew or change our SSH key and password to make sure they are not causing any issues. We can do this with the `ssh-keygen` command.
---
# Getting Help
- The **Hack The Box Forum** is an excellent place for discussing live and retired Hack The Box boxes and challenges.
---
# Knowledge Check
- `searchsploit` (To search for exploits)


# Introduction to Windows
- We can use the `Get-WmiObject` cmdlet to find information about the operating system.
- The **BIOS** is firmware installed on a computer's motherboard that controls the computer's essential functions, such as power management, input/output interfaces, and system configuration.
- `Get-WmiObject` can also be used to start and stop services on local and remote computers, and more.
---
# Accessing Windows
## Local Access Concepts
Local access is the most common way to access any computer, including computers running Windows.
## Remote Access Concepts
Remote Access is accessing a computer over a network. Local access to a computer is needed before one can access another computer remotely.
---
# Most Common Access Technologies
## Remote Desktop Protocol (RDP)
- RDP uses a client/server architecture where a client-side application is used to specify a computer's target IP address or hostname over a network where RDP access is enabled.
- Keep in mind that an **IP address** is used as a logical identifier for a computer on a network, and a **logical port** is an identifier assigned to an application.
- Understand that every computer has an IP address assigned to communicate over a network, and applications hosted on target computers listen on specific logical ports.
---
# Using xfreerdp
We use **xfreerdp** across multiple modules because of its ease of use, feature set, command-line utility, and efficiency.

# MacOS Fundamentals
## What is MacOS?
- In 2000, Apple released a public beta code named Kodiak for users to test and provide feedback.
- Apple released **Mac OS X (10.0)**, named **Cheetah**.
- **iOS XNU Kernel architecture** handles memory, processors, drivers, and other low-level processes.
- **Darwin** is the base of the macOS operating system.
- **Aqua** is the basis for the graphical interface and visual theme for macOS.
- **Finder** is the component of macOS that provides the Desktop experience and file management functions within the OS.
- By default, macOS and any apps within it utilize the concept of **sandboxing**, which restricts the application's access outside of the resources necessary for it to run.
- **Cocoa** is the application management layer and API used with macOS.
---
# File and Directory Permissions
## NIX Permissions Primer
- Within the file system structure, every object on the host belongs to a specific user or group.
- These permissions are shown utilizing the octal or Base 8 numbering system. They are used to apply the read, write, and execute attributes to the contexts of **User owner**, **Group owner**, and **Others** on a file. These are represented as:
    - **Read**: 4
    - **Write**: 2
    - **Execute**: 1
- We can use a **chmod-calculator** that helps do the conversion quickly.
- Using the same file from before, we will modify its ownership by replacing `htb-user` as the owner with `htb-student`. We can do so as follows:
    ```bash
    sudo chown htb-student HTB-Wallpaper-1.png
    ```
    Example output:
    ```bash
    giois@htb[/htb]**$** ls -l 
    -rwxrwxrwx@ 1 htb-student  staff  2512910 Aug 30  2019 HTB-Wallpaper-1.png
    ```
- There is also the **chgrp** command that deals specifically with groups.
---
# Linux Fundamentals

## Getting Help
- In Linux, the `man` command is used to access the manual pages for commands and utilities.

## System Information
- To gather system information, we can use commands like `uname -a` and `lsb_release -a`.

## Navigation
- Use `cd` to change directories, `pwd` to print the current directory, and `ls` to list files in a directory.

## Working with Files and Directories
- You can create directories using `mkdir`, and remove files using `rm`. Use `cp` to copy files and `mv` to move them.

## Editing Files
- Common text editors in Linux include `nano`, `vim`, and `emacs`.

## Find Files and Directories
- The `find` command helps search for files and directories. For example: `find /path/to/search -name "filename"`

## File Descriptors and Redirections
- In Linux, standard input (stdin), output (stdout), and error (stderr) are represented by file descriptors. You can redirect output using `>` and `>>` operators.

## Filter Contents
- You can filter file contents using commands like `grep` to search for specific patterns in files.

## Regular Expressions
- Linux supports regular expressions (regex) for pattern matching in text files, which is often used with commands like `grep`.

## Permissions Management
- Use the `chmod` command to change file permissions and `chown` to change file ownership.

## User Management
- User management can be done using `useradd`, `usermod`, and `userdel` commands to add, modify, and delete users.

## Package Management
- Package management systems like `apt`, `yum`, and `dnf` are used for installing, updating, and removing software packages.

## Service and Process Management
- Use `systemctl` to manage services and `ps`, `top`, and `kill` to manage processes.

## Task Scheduling
- The `cron` and `at` commands are used to schedule tasks to run at specific times.

## Network Services
- Common tools for network services include `netstat`, `ss`, and `ifconfig` for network troubleshooting and configuration.

## Working with Web Services
- To work with web services, tools like `curl` and `wget` are commonly used to retrieve data from web servers.

## Backup and Restore
- Backup tools include `tar`, `rsync`, and `dd` for creating backups, while restore operations are often done using `rsync` or restoring from archives.

## File System Management
- Use commands like `df` to check disk space and `fsck` for file system checks. You can mount file systems with `mount`.

## Containerization
- **Docker** is the most popular tool for containerization in Linux, providing an easy way to deploy applications in isolated environments.

## Network Configuration
- Network configuration can be managed using commands like `ip`, `ifconfig`, and `nmcli`.

## Remote Desktop Protocols in Linux
- Remote desktop services can be accessed via `RDP` using tools like `xrdp`, or through SSH with graphical applications via `X11 forwarding`.

## Linux Security
- Linux security involves tools like `iptables` for firewalls, `selinux` for security policies, and using `chmod`/`chown` for file access control.

## Firewall Setup
- The `iptables` command is commonly used for setting up firewalls on Linux, or you can use `ufw` (Uncomplicated Firewall) for simpler configuration.

## System Logs
- System logs can be found in the `/var/log` directory, with tools like `journalctl` and `dmesg` helping to view system logs and messages.

## Solaris
- Solaris is a Unix-based OS, and commands for managing it are similar to Linux, but with distinct differences, such as `pkg` for package management.

## Shortcuts
- Use keyboard shortcuts like `Ctrl+C` to stop a process, `Ctrl+Z` to suspend a process, and `Ctrl+R` to search command history.

  
# Introduction to Networking
- Outline of my notes taken.
## Network Topologies
- Network topologies describe how devices in a network are connected to each other. Common types include bus, star, ring, and mesh.

## Proxies
- A proxy server acts as an intermediary between a client and a server, handling requests on behalf of the client to improve security, performance, and anonymity.

## Networking Models
- Networking models define how data is transmitted across networks. The two primary models are the OSI model and the TCP/IP model.

## The OSI Model
- The OSI (Open Systems Interconnection) model is a conceptual framework used to understand network interactions in seven layers: Physical, Data Link, Network, Transport, Session, Presentation, and Application.

## The TCP/IP Model
- The TCP/IP model, also known as the Internet model, is a simplified version of the OSI model. It has four layers: Link, Internet, Transport, and Application.

## Network Layer
- The network layer is responsible for routing data across networks. It handles packet forwarding, including IP addressing and routing.

## IP Addresses
- An IP address is a unique identifier for devices on a network, used to route data between them.

## Subnetting
- Subnetting is the process of dividing an IP address into smaller segments called subnets, allowing efficient use of IP addresses and better management of network traffic.

## MAC Addresses
- A MAC (Media Access Control) address is a hardware address used to uniquely identify devices on a local network, operating at the data link layer.

## IPv6 Addresses
- IPv6 is the most recent version of the Internet Protocol, designed to replace IPv4. It uses 128-bit addresses, allowing for a much larger address space.

## Networking Key Terminology
- Key networking terms include bandwidth, latency, throughput, router, switch, gateway, and others essential to understanding network communication.

## Common Protocols
- Common networking protocols include HTTP, FTP, TCP, UDP, IP, ICMP, and DNS, each serving a specific function in data transmission.

## Wireless Networks
- Wireless networks use radio waves to transmit data. Common wireless technologies include Wi-Fi, Bluetooth, and cellular networks.

## Virtual Private Networks (VPNs)
- A VPN encrypts a user's internet traffic and routes it through a server to provide privacy, security, and the ability to bypass geographic restrictions.

## Vendor Specific Information
- Vendor-specific information refers to configurations, protocols, and tools that are unique to specific network hardware or software vendors.

## Key Exchange Mechanisms
- Key exchange mechanisms like Diffie-Hellman are used to securely exchange cryptographic keys over an insecure medium, ensuring secure communications.

## Authentication Protocols
- Authentication protocols, such as Kerberos, RADIUS, and TACACS+, are used to verify the identity of users or devices attempting to access a network.

## TCP/UDP Connections
- TCP (Transmission Control Protocol) is a connection-oriented protocol, while UDP (User Datagram Protocol) is connectionless. TCP ensures reliable data transmission, while UDP offers faster, less reliable communication.

## Cryptography
- Cryptography involves encrypting and decrypting data to protect its confidentiality, integrity, and authenticity. Common techniques include symmetric-key encryption, asymmetric-key encryption, and hashing.


# Javascript Deobfuscation

## Introduction
- JavaScript deobfuscation is the process of reversing the obfuscation applied to JavaScript code to make it more readable and understandable. Obfuscation is typically used to protect code from reverse engineering.

## Source Code
- The source code is the original, unmodified JavaScript code before any obfuscation or minification. Understanding the source code is the first step in the deobfuscation process.

## Code Obfuscation
- Code obfuscation is the practice of modifying the code to make it harder to understand, usually to protect intellectual property or to prevent attackers from exploiting vulnerabilities.

## Basic Obfuscation
- Basic obfuscation involves techniques like renaming variables to meaningless names (e.g., `a`, `b`, `c`), removing comments, and shortening code.

## Advanced Obfuscation
- Advanced obfuscation techniques include using encoding, string manipulation, and control flow flattening to make the code more difficult to reverse-engineer.

## Deobfuscation
- Deobfuscation is the process of transforming obfuscated code back into a readable and understandable format. This often involves manual or automated analysis tools.

## Code Analysis
- Code analysis is crucial for understanding how obfuscated code works. Techniques such as debugging, static analysis, and dynamic analysis can be used to inspect the behavior of the code.

## HTTP Requests
- Understanding how the obfuscated code interacts with the server through HTTP requests is an essential part of the deobfuscation process. This can help to identify any hidden functionalities or vulnerabilities.

## Decoding
- Decoding is the process of reversing encoded values in the obfuscated code. This could include Base64, URL encoding, or custom encoding methods used to obfuscate strings or variables.



# Using the Metasploit Framework

## Introduction

### Preface
- The Metasploit Framework is one of the most widely used tools for penetration testing and exploitation. It provides a collection of tools for discovering, exploiting, and validating vulnerabilities in systems.

### Introduction to Metasploit
- Metasploit is an open-source framework that provides penetration testers with an integrated environment to conduct security assessments. It has a variety of modules designed for different tasks, such as exploiting vulnerabilities, gaining access, and escalating privileges.

### Introduction to msfconsole
- `msfconsole` is the primary interface used to interact with the Metasploit Framework. It is a command-line tool that provides access to all Metasploit features, from launching exploits to managing sessions.

## MSF Components

### Modules
- Metasploit modules are pre-written pieces of code that perform specific tasks, such as exploiting vulnerabilities or performing post-exploitation tasks. There are several types of modules, including exploit, auxiliary, and post modules.

### Targets
- Targets define the specific system or application that is being attacked. When using Metasploit, you need to select the appropriate target for the exploit.

### Payloads
- Payloads are the pieces of code that are executed after a successful exploit. They provide functionality like creating a reverse shell, uploading a backdoor, or running commands on the target system.

### Encoders
- Encoders are used to modify payloads to evade detection by security mechanisms like antivirus software or firewalls. They obfuscate the payload to avoid signature-based detection.

### Databases
- Metasploit integrates with databases to store information about discovered vulnerabilities, exploited systems, and sessions. This allows penetration testers to keep track of their findings and progress.

### Plugins & Mixes
- Plugins extend Metasploit's functionality, allowing it to integrate with other tools or add custom features. Mixes are a set of plugins that work together to perform specific tasks.

## MSF Sessions

### Sessions & Jobs
- A session in Metasploit refers to an active connection between your attacking machine and the target. Jobs are tasks that run in the background, such as launching exploits or handling multiple sessions.

### Meterpreter
- Meterpreter is a powerful payload that provides an interactive shell on the target system. It allows for advanced post-exploitation tasks like privilege escalation, file manipulation, and keystroke logging.

## Additional Features

### Writing & Importing Modules
- Metasploit allows users to write custom modules to extend its capabilities. These modules can be written in Ruby and imported into the framework for use in penetration tests.

### Introduction to MSFVenom
- MSFVenom is a tool used to generate various types of payloads. It combines the functionality of Metasploit's `msfpayload` and `msfencode` tools, providing an easy-to-use interface for creating payloads.

### Firewall and IDS/IPS Evasion
- Metasploit includes features to help evade firewalls and intrusion detection/prevention systems (IDS/IPS). These techniques involve obfuscating traffic or using alternative protocols to avoid detection.

### Metasploit-Framework Updates - August 2020
- The Metasploit Framework is constantly updated with new features, bug fixes, and exploit modules. In August 2020, several updates were made, including improved support for modern payloads, new exploits, and enhanced evasion techniques.



# Stack-Based Buffer Overflows on Linux x86

## Introduction

### Buffer Overflows Overview
- A buffer overflow occurs when data overflows from one buffer to the next in memory. In the context of security, this can allow an attacker to overwrite parts of the memory with malicious code or data.

### Exploit Development Introduction
- Exploit development involves crafting a series of steps to exploit vulnerabilities, such as buffer overflows, in software. It requires knowledge of the underlying architecture and how to manipulate program execution.

### CPU Architecture
- The CPU architecture defines the structure and behavior of the CPU. On Linux x86 systems, the architecture is based on the Intel/AMD processor family, with 32-bit memory addressing and specific instruction sets.

## Fundamentals

### Stack-Based Buffer Overflow
- A stack-based buffer overflow occurs when data written to a buffer on the stack overflows into adjacent memory. This can overwrite control information, such as function return addresses, and allow for arbitrary code execution.

### CPU Registers
- CPU registers are small storage locations within the processor used for quick data access. In the context of buffer overflows, registers like the EIP (Instruction Pointer) are crucial because overwriting them can change the flow of execution.

## Exploit

### Take Control of EIP
- By overwriting the EIP register, an attacker can redirect the program's execution flow to their malicious code. This is the key objective of most stack-based buffer overflow exploits.

### Determine the Length for Shellcode
- Shellcode is a small piece of code that is injected into a buffer during a buffer overflow attack. To successfully execute the shellcode, you must calculate the precise length of data to overflow the buffer and place the shellcode in the right location.

### Identification of Bad Characters
- Bad characters are specific bytes that may interfere with the execution of shellcode. Identifying and avoiding these characters is essential to ensure that the payload works as intended.

### Generating Shellcode
- Shellcode is typically written in assembly language and designed to perform specific actions, such as spawning a shell or adding a new user. Tools like `msfvenom` can be used to generate shellcode.

### Identification of the Return Address
- The return address is the value in the stack that tells the program where to return after a function finishes executing. By identifying and modifying the return address, an attacker can redirect the flow of execution.

## Proof-of-Concept

### Public Exploit Modification
- Public exploits can be modified to suit specific environments or applications. This typically involves adjusting the shellcode, buffer size, and return address to match the target system.

### Prevention Techniques and Mechanisms
- Several techniques can help prevent stack-based buffer overflow attacks, including:
  - Stack canaries: Special values placed on the stack to detect overflows.
  - ASLR (Address Space Layout Randomization): Randomizing memory locations to make it difficult for an attacker to predict buffer locations.
  - DEP (Data Execution Prevention): Preventing certain areas of memory from being executed as code.


# SQL Injection Fundamentals

## Introduction
- SQL Injection (SQLi) is a code injection technique that exploits vulnerabilities in an application's software by manipulating SQL queries. Attackers can use this to execute arbitrary SQL code and gain unauthorized access to databases.

## Databases

### Intro to Databases
- A database is a structured collection of data that is stored and accessed electronically. Databases are typically managed by Database Management Systems (DBMS), which handle data storage, retrieval, and manipulation.

### Types of Databases
- There are several types of databases, including:
  - **Relational Databases (RDBMS):** Use tables to store data and SQL (Structured Query Language) to manage it. Examples include MySQL, PostgreSQL, and SQLite.
  - **NoSQL Databases:** Store data in non-tabular forms, such as key-value pairs, documents, or graphs. Examples include MongoDB, Redis, and Cassandra.
  - **In-memory Databases:** Store data in RAM for quick access, such as Redis or Memcached.

## MySQL

### Intro to MySQL
- MySQL is an open-source relational database management system that uses SQL for querying and managing data. It's one of the most popular databases for web applications.

### SQL Statements
- SQL statements are used to interact with databases. Common SQL statements include:
  - **SELECT:** Retrieves data from a database.
  - **INSERT:** Adds new data to a database.
  - **UPDATE:** Modifies existing data.
  - **DELETE:** Removes data from a database.

### Query Results
- Query results in MySQL are typically returned in tabular form. They can be processed by the application or displayed to users through a web interface.

### SQL Operators
- SQL operators are symbols that perform operations on data. Common SQL operators include:
  - **=** (Equal)
  - **>** (Greater than)
  - **<** (Less than)
  - **AND** and **OR** (Logical operations)
  - **LIKE** (Pattern matching)

## SQL Injections

### Intro to SQL Injections
- SQL injection occurs when an attacker manipulates a web application's input fields to send unauthorized SQL queries to the database. This can lead to unauthorized data access, modification, and even full system compromise.

### Subverting Query Logic
- Attackers can manipulate the logic of a query by injecting malicious SQL code. For example:
  - **Normal Query:** `SELECT * FROM users WHERE username = 'admin' AND password = 'password'`
  - **Injected Query:** `SELECT * FROM users WHERE username = '' OR '1'='1' --`

### Using Comments
- SQL comments can be used to bypass portions of a query, making it easier for attackers to manipulate the logic:
  - Single-line comment: `--`
  - Multi-line comment: `/* comment */`

### Union Clause
- The `UNION` SQL operator allows an attacker to combine the results of multiple queries. This can be used to extract data from other tables in the database:
  - Example: `SELECT column1, column2 FROM table1 UNION SELECT column1, column2 FROM table2`

### Union Injection
- Union-based SQL injection exploits the `UNION` operator to fetch data from other tables. Attackers can combine the output of their injection with legitimate query results to reveal sensitive information.

## Exploitation

### Database Enumeration
- Database enumeration involves identifying the structure of a database, such as table names, column names, and data types, by injecting SQL code into application inputs.

### Reading Files
- Attackers can use SQL injection to read files from the server's filesystem. This is often done by using SQL functions like `LOAD_FILE()` to read local files:
  - Example: `SELECT LOAD_FILE('/etc/passwd')`

### Writing Files
- In some cases, SQL injection can allow attackers to write files to the system, which could lead to further exploitation, such as upl



# Stack-Based Buffer Overflows on Windows x86

## Buffer Overflow
- A buffer overflow occurs when data overflows from one memory location to another, overwriting adjacent memory. This can lead to unexpected behaviors, including program crashes or code execution vulnerabilities, where an attacker can execute arbitrary code by exploiting this flaw.

## Debugging Windows Programs
- Debugging Windows programs is a crucial skill when working with buffer overflow vulnerabilities. Tools such as **OllyDbg** and **Immunity Debugger** can help analyze the flow of execution and monitor the contents of memory and registers to identify overflows and the location of buffer overflows.
  - **Visual Studio Debugger** can also be used to step through code to understand how data is handled and where overflows occur.
  - **Windows Debugging Tools (WinDbg)** are useful for debugging both user-mode and kernel-mode code, especially in a more complex system environment.

## Local Buffer Overflow
- A **local buffer overflow** happens when an attacker sends malicious data to a program running on their own machine, which causes the program to crash or execute unauthorized code. In a local overflow, the attacker typically already has access to the system and exploits the vulnerability for code execution.
  - This is usually easier to exploit than remote overflows, as the attacker has direct control over the environment.

## Remote Buffer Overflow
- A **remote buffer overflow** occurs when an attacker sends specially crafted input to a program running on a remote machine. This type of overflow is more dangerous as it does not require physical access to the machine and can be used to compromise systems over the internet.
  - **Exploiting remote overflows** typically involves sending data over a network, such as through HTTP requests, to overflow a buffer and take control of the machine.


# Brief Intro to Hardware Attacks

## Introduction
- Hardware attacks target the physical components of a computer or device. These attacks exploit vulnerabilities in the hardware or the way it interacts with software. They can range from tampering with circuit boards to exploiting electromagnetic radiation. Hardware attacks are critical in securing devices, especially in environments where high-security systems are used.

## Bluetooth Attacks

### Introduction to Bluetooth
- Bluetooth is a wireless technology used for exchanging data over short distances. It operates on the 2.4 GHz ISM band and is commonly found in mobile phones, computers, and other wireless devices. Despite its convenience, Bluetooth is prone to various security flaws.

### Bluetooth Legacy Attacks
- **Bluejacking**: Sending unsolicited messages to Bluetooth-enabled devices.
- **Bluesnarfing**: Unauthorized access to data on a Bluetooth-enabled device.
- **Bluebugging**: Gaining control over a Bluetooth device to make calls or send messages without the user’s knowledge.

### Modern Bluetooth Attacks and Mitigation
- **BLE (Bluetooth Low Energy) Spoofing**: Attackers impersonate legitimate Bluetooth Low Energy devices to intercept communication.
- **Man-in-the-Middle (MITM) Attacks**: Intercepting and altering data in Bluetooth communication.
- **Mitigation**: 
  - Use of stronger encryption and pairing mechanisms (e.g., AES-128).
  - Regularly update Bluetooth firmware.
  - Disable Bluetooth when not in use.
  - Implement secure pairing and authentication methods (e.g., Passkey Entry).

## Cryptanalysis Side-Channel Attacks

### Introduction to Cryptanalysis
- Cryptanalysis is the study of analyzing and breaking cryptographic systems. Side-channel attacks are a subset of cryptanalysis where attackers exploit physical information (e.g., time, power consumption, electromagnetic emissions) emitted during the operation of a cryptographic system to gain information about the secret keys or data.

### Cryptanalysis Side-Channel Attacks
- **Timing Attacks**: Measuring the time taken for cryptographic operations to reveal information about the key.
- **Power Analysis**: Observing the power consumption of a device while performing cryptographic operations to extract secrets.
- **Electromagnetic (EM) Attacks**: Capturing electromagnetic emissions to extract cryptographic keys or data.
- **Mitigation**:
  - Use constant-time algorithms to prevent timing attacks.
  - Implement power and EM shielding to protect against power and EM analysis.
  - Introduce noise into power consumption patterns to make side-channel data less predictable.

## Microprocessor Vulnerabilities

### Understanding Microprocessors
- A **microprocessor** is the central processing unit (CPU) of a computer, responsible for executing instructions from programs. Modern microprocessors are highly complex and capable of performing billions of operations per second.

### Microprocessor Vulnerabilities
- **Meltdown** and **Spectre**: These vulnerabilities allow attackers to read sensitive information from the memory by exploiting speculative execution and out-of-order execution techniques.
- **Rowhammer**: A hardware vulnerability where repeatedly accessing certain memory locations can cause bit flips in adjacent memory, potentially leading to privilege escalation.
- **Cold Boot Attacks**: Attacking the contents of a system’s memory by physically accessing it, often performed on systems with no disk encryption.
- **Mitigation**:
  - Apply CPU microcode patches to mitigate known vulnerabilities.
  - Use physical security measures to protect hardware.
  - Implement software techniques such as memory encryption to make attacks more difficult.
 
# Web Fuzzing

## Introduction
- Web fuzzing is a technique used to identify vulnerabilities in web applications by sending a large amount of random or unexpected data (fuzz) to the application. The goal is to find security weaknesses that can be exploited by attackers, such as input validation errors, buffer overflows, or other vulnerabilities that can lead to unauthorized access.

## Directory and File Fuzzing

### Directory and File Fuzzing
- Directory and file fuzzing involves sending requests for various directory and file names to identify hidden or unauthorized files and directories on a web server. This can uncover configuration files, backup files, or other sensitive information.

### Recursive Fuzzing
- Recursive fuzzing is an advanced method where the fuzzing process is repeated at deeper levels within directories. This helps to identify files or directories buried deeper in the server structure that may not be visible in a simple directory listing.

## Parameter and Value Fuzzing

### Parameter and Value Fuzzing
- Parameter and value fuzzing focuses on testing URL parameters, form inputs, and headers by injecting random or unexpected data. This technique aims to discover vulnerabilities like SQL injection, cross-site scripting (XSS), or buffer overflows in the web application’s input handling mechanisms.

## Virtual Host and Subdomain Fuzzing

### Virtual Host and Subdomain Fuzzing
- Virtual Host and Subdomain fuzzing involves sending requests with various subdomains or virtual host names to identify additional, hidden domains or services running on a server. This can help in discovering poorly configured servers or forgotten subdomains that could be a point of attack.

## Filtering Fuzzing Output

### Filtering Fuzzing Output
- After performing fuzzing, the output can often be overwhelming and cluttered. Filtering fuzzing output helps to focus on the most relevant findings, making it easier to identify potential vulnerabilities. This can involve filtering by response status codes, response time, or specific patterns that indicate unusual behavior.

## Validating Findings
- Once vulnerabilities are identified, they must be validated to ensure they are legitimate and not false positives. This involves manually testing the findings and verifying that the application behaves as expected under the injected data. Proper validation ensures that fuzzing efforts lead to actionable security improvements.

## Web APIs

### Web APIs
- Web APIs (Application Programming Interfaces) allow communication between different software components over the web. These APIs are integral to modern web applications, providing a way for different systems to interact programmatically.

### Identifying Endpoints
- Identifying API endpoints is critical for testing web APIs. This involves discovering the URL paths and methods that are exposed by the application. These endpoints are where the application processes incoming requests, and they often serve as attack surfaces for various vulnerabilities.

### API Fuzzing
- API fuzzing targets the inputs and parameters of web APIs to detect vulnerabilities. This includes testing parameters, headers, and request bodies with random or unexpected data to find flaws in input validation or data handling within the API.



# Introduction to Bash Scripting

## Introduction
- Bash scripting is a powerful way to automate tasks and manage system operations in Linux and other UNIX-like operating systems. It allows users to execute commands and scripts in the terminal, providing control over processes, files, and other system components.

## Working Components

### Conditional Execution
- Conditional execution in Bash scripting is used to execute commands or scripts based on certain conditions. This is typically done using `if`, `elif`, `else`, and `case` statements to make decisions.

### Arguments, Variables, and Arrays
- **Arguments:** These are values passed to a script when it's executed, typically via the command line. For example, `$1`, `$2`, etc., represent the arguments passed to the script.
- **Variables:** Variables are used to store data and can be assigned using the syntax `variable_name=value`.
- **Arrays:** Arrays allow for storing multiple values in a single variable. They are defined using the syntax `array_name=(value1 value2 value3)`.

### Comparison Operators
- Bash provides a variety of comparison operators for strings, integers, and file attributes. Some examples:
  - String comparison: `==`, `!=`
  - Integer comparison: `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`
  - File comparison: `-e` (exists), `-d` (directory), `-f` (file), etc.

### Arithmetic
- Bash allows you to perform arithmetic operations using `((expression))` or `let expression`. Common arithmetic operations include addition `+`, subtraction `-`, multiplication `*`, division `/`, and modulus `%`.

## Script Control

### Input and Output Control
- **Input:** You can read input from the user using the `read` command. For example, `read variable_name` waits for user input and stores it in the specified variable.
- **Output:** Output can be displayed using `echo` or `printf` for more formatted control.

### Flow Control - Loops
- Loops are used for repeating a set of commands. The common loop structures are:
  - **`for` loop:** Loops through a set of values.
  - **`while` loop:** Continues looping as long as a condition is true.
  - **`until` loop:** Loops until a condition becomes true.

### Flow Control - Branches
- Branching allows for decision-making in scripts. The common branching structures are:
  - **`if` statement:** Executes a block of code if a condition is true.
  - **`else` and `elif`:** Provide alternate blocks of code when conditions aren't met.

## Execution Flow

### Functions
- Functions in Bash are blocks of reusable code. They are defined with the syntax:
  ```bash
  function_name () {
    # Commands
  }

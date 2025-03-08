---
layout: default
title: "LetsDefend Notes"
---

# 🛡️ LetsDefend Notes

This page contains my notes on LetsDefend challenges and investigations.

### Malicious AutoIT

- **HashCalc Tool** to calculate MD5 of this sample.
- Put the Hash in VirusTotal.
  
#### AutoIT
- Automating the Windows GUI means using a script to interact with Windows applications and system elements just like a human would.

#### Entropy in File Analysis
- **Entropy** measures the randomness or unpredictability of data in a file.
    - **Low entropy (~0 to 5)**: The file contains a lot of readable text or structured data.
    - **High entropy (~7 to 8)**: The file is likely compressed, encrypted, or packed (often used by malware to obfuscate its contents).

#### Time Date Stamp (TDS)
- According to the Detect Easy tool, what is the "time date stamp"?
    - **Malware Analysis**: Helps identify when a sample was created or modified.
    - **Threat Hunting**: Can be correlated with known malicious campaigns.
    - **Reverse Engineering**: Can give hints about the toolchain used to build the executable.

#### Entry Point Address
- According to the Detect It Easy (DIE) tool, what is the entry point address of the executable?
    - **Entry Point Address** is the memory address where a program starts executing when loaded into memory.

#### Malicious Embedded Code Domain
- What is the domain used by the malicious embedded code?
    - **Packed Files**: These are compressed or encrypted to obscure their contents from security tools like antivirus software.
    - **Unpacking**: The process of removing this protection (e.g., decompressing, decrypting) to analyze the actual code and determine what the file does.
    - **AutoIt-Ripper**: A Python script that can extract a compiled AutoIt sample.
    - The domain `office-cleaner-commander.com` looks like a potentially malicious domain and could be associated with malicious activity or malware.

#### File Path Encoded in Hexadecimal
- What is the file path encoded in hexadecimal in the malicious code?
    - `:\Windows\System32\`
    - **Hiding Malicious Files**: Malware may use the System32 path to hide its files and make them appear legitimate.
    - **Persistence**: Files in System32 could be used for persistence mechanisms, meaning the malware stays active even after a reboot.

#### Name of the DLL Called by the Malicious Code
- What is the name of the DLL called by the malicious code?
    - **user32.dll**
    - Malware often uses legitimate Windows functions to avoid detection. If malware calls `user32.dll`, it might be attempting to use Windows API functions for malicious purposes while appearing like a normal system process.

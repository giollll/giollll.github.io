---
layout: default
title: "PicoCTF Notes"
---

# 🏆 PicoCTF Notes

This page contains my notes and solutions for various challenges in PicoCTF, categorized by topic.

## 📌 Categories

- [🟢 Primer](./primer.md)
Web Exploitation
    GET aHEAD
        burpsuite
        Proxy⇒ Open Browser⇒Intercept On
        History of requests made.
        Response Headers. Request Headers.
    WebDecode
        Inspect (right-click ⇒ inspect) the "about" page
        There should be a base64 encoded string.
        Put that into chatgpt or cyberchef
    Unminify
        Open the site and "view page source"
        The flag should be there
        or
        curl <the_website_link>
        cat index.html (The flag should be there)
    IntroToBurp
        Use burpsuite web browser
        Get through until the otp request
        Take out the "otp=" line
        It should give you the flag. We basically bypassed the otp request. 
Cryptography 
    Cyber chef
    CSR decoder
    HideToSee
        steghide extract -sf <file> 
Reverse Engineering 
Forensics
    Verify
        ssh into the machine
        use the password given
        I did sha256sum files/* (to get the hash of each file)
        sha256sum files/* | grep 467 (to find the file that has the same hash)
        Then ran ./decrypt.sh /files/c6c8b911 (This should reveal the flag)
    Scan Surprise
        Copied the link to the zipped file: wget <copied.zip.file>
        unzip <zipped.file>
        Went to directory: /ctf-player/drop-in
        Moved flag.png to my Downloads folder.
        Opened the png with my file viewer and scanned the qr code with my phone to reveal the flag. 
    Secret of the Polyglot
        Download and open the file
        file <file_name> (To see what type of file it is)
        cp <file_name>.pdf <file_name>.png
        Now you should open both files in file viewer
        Combine!
    interencdec
        Download the file
        cat the contents and copy the text
        Paste it into cyberchef
        Do, "From base64"
        Copy the text within the single quotes and paste it into cyberchef.
        Copy and paste, the new text and now use rot 19.
        The flag should be displayed. 
General Skills
    Binary Search
        SSH into the machine
        Guess the number that's halfway between.
        1-1000: Guess 500, if its lower
        Guess 250, If its higher, guess midway between 250-500
        375, If its higher, guess between 375-50


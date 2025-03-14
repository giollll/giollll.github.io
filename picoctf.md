---
layout: default
title: "PicoCTF Notes :)"
---

# 🏆 PicoCTF Notes

This page contains my notes and solutions for various challenges in PicoCTF, categorized by topic.

## 📌 Categories

- [🟢 Primer](./primer.md)

  
# PicoCTF Notes

🏆 **PicoCTF Notes**  
This page contains my notes and solutions for various challenges in PicoCTF, categorized by topic.

## 📌 Categories

### 🟢 **Primer**

#### **Web Exploitation**
- **GET aHEAD**
  - burpsuite
  - Proxy ⇒ Open Browser ⇒ Intercept On
  - History of requests made.
  - Response Headers. Request Headers.
- **WebDecode**
  - Inspect (right-click ⇒ inspect) the "about" page
  - There should be a base64 encoded string.
  - Put that into ChatGPT or Cyberchef.
- **Unminify**
  - Open the site and "view page source".
  - The flag should be there.
  - Or curl `<the_website_link>`.
  - `cat index.html` (The flag should be there).
- **IntroToBurp**
  - Use burpsuite web browser.
  - Get through until the otp request.
  - Take out the "otp=" line.
  - It should give you the flag. We basically bypassed the OTP request.
- ## Bookmarklet
1. Go to bookmarks and right-click on **"All Bookmarks"**, then select **"Add Page"** (Chrome).
2. Set the name as **"Find Flag"**.
3. Copy and paste the JavaScript code, save it, then click on it.
4. It should give you the flag.

- **Note:**  
Bookmarklets are JavaScript scripts saved as browser bookmarks. They run on the webpage you're viewing, allowing you to automate tasks or extract information, but only affect your view.

- ## Local Authority
1. Use the login website and trigger a failed login attempt.
2. Inspect the page and look into **Sources**.
3. There should be a program that reveals a **username and password**.
4. Use that username and password to log in.
5. Once logged in, the flag should be displayed.

- ## Inspect HTML
1. Open the website.
2. Right-click and select **Inspect**.
3. Navigate to the **Sources** tab.
4. The flag should be there.

- ## Includes
1. Go to the website and inspect the page.
2. Look into **Sources**.
3. Check the two different files—parts of the flag should be there.

- ## Cookies
1. Open the website and inspect it.
2. Locate the **cookie** that exists on the website.
3. Find the **cookie ID** and modify it (try values from `1-18`) until you find the flag.

- ## Scavenger Hunt
1. Go to the website and **view page source**.
2. Inspect the **Sources** tab.
3. Look into:
   - **robots.txt** – Can reveal hidden or restricted directories.
   - **.htaccess** – May contain access control rules.
   - **.DS_Store** – A macOS metadata file that stores information about how files are arranged in a directory (icons, positions, etc.).

#### **Cryptography**
- **Cyber chef**
- **CSR decoder**
- **HideToSee**
  - `steghide extract -sf <file>` 

#### **Reverse Engineering**

#### **Forensics**
- **Verify**
  - SSH into the machine.
  - Use the password given.
  - I did `sha256sum files/*` (to get the hash of each file).
  - `sha256sum files/* | grep 467` (to find the file that has the same hash).
  - Then ran `./decrypt.sh /files/c6c8b911` (This should reveal the flag).
- **Scan Surprise**
  - Copied the link to the zipped file: `wget <copied.zip.file>`.
  - `unzip <zipped.file>`.
  - Went to directory: `/ctf-player/drop-in`.
  - Moved `flag.png` to my Downloads folder.
  - Opened the png with my file viewer and scanned the QR code with my phone to reveal the flag.
- **Secret of the Polyglot**
  - Download and open the file.
  - `file <file_name>` (To see what type of file it is).
  - `cp <file_name>.pdf <file_name>.png`.
  - Now you should open both files in the file viewer.
  - Combine!
- **interencdec**
  - Download the file.
  - `cat` the contents and copy the text.
  - Paste it into Cyberchef.
  - Do, "From base64".
  - Copy the text within the single quotes and paste it into Cyberchef.
  - Copy and paste the new text and now use ROT 19.
  - The flag should be displayed.

#### **General Skills**
- **Binary Search**
  - SSH into the machine.
  - Guess the number that's halfway between.
  - 1-1000: Guess 500, if it's lower.
  - Guess 250, if it's higher, guess midway between 250-500.
  - 375, if it's higher, guess between 375-500, and so on, until you find the number.
- **Time Machine**
  - Download and unzip the file.
  - Look for hidden directories and go into that hidden directory.
  - Do: `cat COMMIT_EDITMSG`.
- **Super SSH**
  - `ssh -p 57714 ctf-player@titan.picoctf.net` (To get a shell).
  - Use the password and it should give you the flag once you get in.
- **endianness**
  - **Little endian**: Convert characters to hex, arrange them reverse of Big Endian.
  - **Big Endian**: Convert characters to hex, bunch them together, that's the answer.

#### **Binary Exploitation**
- **heap 0**
  - Write to the buffer and fill it as much as possible until `bico` is no longer `bico` but what you wrote in.
  - Write this to the buffer and it should work: `11111111111111111111111`.
  - Then print out the flag.
- **format string 0**
  - Just enter 34+ 0's and it should give you the flag at some point.

#### **Uncategorized**

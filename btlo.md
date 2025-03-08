---
layout: default
title: "BTLO Notes"
---

# 🛡️ BTLO Notes

This page contains my notes on BTLO challenges and investigations focused on blue team skills.

## 📌 Investigations
# PowerShell Analysis - Keylogger

## To find the SHA256 value
- Unzip file: password = `btlo`
- Inner file password = `infected`
- `sha256sum <path_to_file> <file_name>`

## To find the email address
- Simply `cat` out the file
- Next to: `"From"`

## Finding the email password
- Found the credentials `=` where `$Pass` is included
- I did `cat <file_name> | grep Pass` and the password appeared.

## To find the DLL
- `cat <file_name> | grep .dll`

## To find the directory the txt file is put in
- `cat <file_name> | grep .txt`

# The Report
- `Ctrl + f` the entire document

# Tusk Infostealer Lab

## How to get the size of a file
- Get the MD5 from the `.txt` file and then go to VirusTotal and paste the MD5 to get the file size.

# Follina

## Get the SHA1 hash value
- `sha1sum <file_name>`

## Get the file type
- Go to details, should be next to "File type" 

## Extract the URL
- Go to behavior and go to HTTP requests (On VirusTotal)

## Finding the name of the XML file that is storing the extracted URL
- Go to relations
- Under Bundled files

# Rapid Response: Microsoft Office RCE - “Follina” MSDT Attack | Huntress
- Use the report above to answer 5-7
- Look at Behavior
  - Expand the execution portion, should be there.

---
layout: default
title: "NCAE Tutorials Notes"
---

# 📚 NCAE Tutorials Notes

This page contains my notes on various tutorials from the NCAE platform.

## Change All User Passwords
- CH-DC/herdening/linux/main/INIT/credentialRotate.sh at main · USF-Computer-Science-and-Engineering/CH-DC · GitHub

## Backup
- Hide /dev
- Check if sources are up
- Keep `pspy` running continuously

## Network Configuration

### Router (CentOS)
- Edit external network interface:
    ```bash
    sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0
    ```
- Edit internal network interface:
    ```bash
    sudo vi /etc/sysconfig/network-scripts/ifcfg-eth1
    ```
- List all firewall rules:
    ```bash
    sudo firewall-cmd --list-all --zone=external
    ```
- Add port forwarding:
    ```bash
    sudo firewall-cmd --zone=external --permanent --add-forward-port=port=80:proto=tcp:toport=80:toaddr=<given_IP>
    sudo firewall-cmd --reload
    ```
- Verify port forwarding:
    ```bash
    sudo firewall-cmd --list-all --zone=external
    ```

### Web Server (Internal Web Server, Ubuntu)
- View IP addresses:
    ```bash
    ip a
    ```
- Configure network settings:
    ```bash
    sudo nano /etc/netplan/01-network-manager-all.yaml
    ```
- Indentation with two spaces, `addresses` and `gateway4` at the same indent level:
    ```yaml
    ethernets:
      ens18:
        addresses:
          - <given_ip>
        gateway4: <router_external_ip>
    ```
- Apply changes:
    ```bash
    sudo netplan apply
    ```
- Check Apache status:
    ```bash
    systemctl status apache2
    ```
- Start Apache if necessary:
    ```bash
    sudo systemctl start apache2
    ```
- Edit the webpage:
    ```bash
    sudo nano /var/www/html/index.html
    ```

### Internal Kali
- Edit network settings:
    ```bash
    sudo nano /etc/network/interfaces
    ```
- Set up static IP for eth0:
    ```bash
    auto eth0
    iface eth0 inet static
    ```
- Restart networking service:
    ```bash
    sudo systemctl restart networking
    ```
- Check IP address:
    ```bash
    ip a
    ```

## SSH Configuration
- Check SSH status:
    ```bash
    systemctl status ssh
    ```
- Edit SSH config:
    ```bash
    cd /etc/ssh
    nano /etc/ssh/ssh_config
    ```
- Edit SSH daemon config:
    ```bash
    nano /etc/ssh/sshd_config
    ```
- Disable root login:
    ```bash
    PermitRootLogin no
    ```
- Test connection:
    ```bash
    ssh sandbox@<ip_of_ssh_machine>
    ```
- To terminate SSH session:
    ```bash
    exit
    ```

### SSH Keys Setup
- Generate new SSH keys:
    ```bash
    sudo ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
    ```
- Create passwordless authentication for a new user:
    ```bash
    sudo adduser bob
    password
    ssh bob@<ip>
    password: password
    ```
- Generate SSH key for `bob`:
    ```bash
    sudo ssh-keygen -t ecdsa -f ~/id_bob_key
    ```
- Create `.ssh` directory for `bob`:
    ```bash
    mkdir /home/bob/.ssh
    sudo cp id_bob_key.pub /home/bob/.ssh/authorized_keys
    ```
- Adjust permissions for SSH key:
    ```bash
    sudo chmod 700 /home/bob/.ssh
    sudo chown bob:bob /home/bob/.ssh
    sudo chown bob:bob /home/bob/.ssh/authorized_keys
    ```
- Transfer key to another machine:
    ```bash
    sudo chown sandbox:sandbox id_bob_key
    scp sandbox@<computer_ip>:/home/sandbox/id_bob_key .
    ssh -i /home/sandbox/id_bob_key bob@<given_ip>
    ```
- Easier way to copy SSH key:
    ```bash
    sudo ssh-keygen -t ecdsa -f /home/sandbox/id_sandbox_key
    sudo ssh-copy-id -i id_sandbox_key sandbox@<given_ip>
    ```

### SSH Service through the Router
- SSH service check:
    ```bash
    systemctl status sshd
    ip a
    sudo firewall-cmd --list-all --zone=internal
    ```
- Removing SSH service from external:
    ```bash
    sudo firewall-cmd --list-all --zone=external --permanent --remove-service=ssh
    sudo firewall-cmd --reload
    ```
- Adding SSH service to external:
    ```bash
    sudo firewall-cmd --list-all --zone=external --permanent --add-service=ssh
    sudo firewall-cmd --reload
    ```
- SSH forwarding on router:
    ```bash
    sudo firewall-cmd --zone=external --permanent --add-forward-port=port=22:proto=tcp:toport=22:toaddr=<internal_IP_router>
    sudo firewall-cmd --reload
    ```

## Rsync Service Basics
- Backing up files:
    ```bash
    mkdir stuff
    touch stuff/practice stuff/practice2
    mkdir backups
    rsync -av --delete stuff/ backups/.
    ```
- Verify files:
    ```bash
    echo james was here >> stuff/practice
    rsync -av --delete stuff/ backups/.
    ```

## Cron Service
- Edit cron jobs:
    ```bash
    crontab -e
    ls /etc/crontab
    ```

## Rsync and Cron
- Setting up Rsync in cron:
    ```bash
    rsync -av -e ssh <file_path> <user>@<ip>:<location_for_backups>
    sudo ssh-keygen -t ecdsa -f backup_keys
    sudo chown root:root backup_keys
    sudo mv backup_keys /root
    scp backup_keys.pub <user>@<ip>:/home
    ```
- On server:
    ```bash
    mkdir .ssh
    cp backup_keys.pub ~/.ssh/authorized_keys
    ```
- Rsync with key authentication:
    ```bash
    rsync -av -e "ssh -i /root/backup_keys" <our_files_path> <user>@<server_IP>:<backup_file_path>
    ```
- Setting up cron:
    ```bash
    sudo nano /etc/crontab
    . * * * * * root rsync -av -e "ssh -i /root/backup_keys" <our_files><user>@<ip_server_backup>:/backup/path
    ```

## Firewalls
- Internal machines firewall setup:
    ```bash
    sudo ufw status
    sudo iptables (on Kali)
    sudo ufw enable
    sudo ufw allow from 192.168.195.100
    sudo ufw deny from 192.168.195.0/24
    sudo ufw status verbose
    sudo ufw allow ssh
    sudo ufw status numbered
    sudo ufw delete 4
    ```
- Modify firewall rules:
    ```bash
    sudo nano /etc/ufw/before.rules
    sudo ufw reload
    ```
- Reset firewall:
    ```bash
    sudo ufw reset
    ```

## Active Connection Defense
- Checking active connections:
    ```bash
    netstat -tu
    netstat -tun
    sudo netstat -tunap
    ```
- Kill suspicious connections:
    ```bash
    sudo kill <PID#>
    ```
- List who is logged in:
    ```bash
    w
    sudo pkill -KILL -u jenny
    ```

## Scripting
- Basic script:
    ```bash
    touch my_first_script.sh
    nano my_first_script.sh
    #!/bin/bash
    echo Hello World
    ls -l
    chmod 755 my_first_script.sh
    ./my_first_script.sh
    ```
- Advanced script:
    ```bash
    msg="Hello World!"
    echo "This script says: $msg"
    read -p "Enter your second message: " msg2
    echo "Your second message was: $msg2"
    ```

- Scripting file creation:
    ```bash
    echo "The user typed: $msg2" >> output.txt
    ./my_first_script.sh
    ```

- Running script from a different directory:
    ```bash
    mv my_first_script.sh Documents/
    /home/sandbox/Documents/my_first_script.sh
    cd Documents/
    ```

- Script for IP changer:
    ```bash
    cp /etc/network/interfaces .
    nano interfaces
    #!/bin/bash
    path=/etc/network/interfaces
    read -p "Please enter the desired IP: " ip
    read -p "Please enter the desired mask: " mask
    echo "auto eth0" >> $path
    echo "iface eth0 inet static" >> $path
    echo "    address $ip" >> $path
    echo "    netmask $mask" >> $path
    systemctl restart networking
    ip a
    chmod +x interfaces
    mv interfaces interfaces.sh
    sudo ./interfaces.sh
    ```

## MikroTik Router and Mini Hack Completion
- Login to router:
    ```bash
    ip a
    ```

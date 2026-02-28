First of all we check that we have connection with IP target.
```bash
$ ping -c 1 10.129.229.41
```
![alt text](Images/Ping.png)

This TTL value on HTB indicates that is a Linux machine.

We will start with our usual Nmap scan and find the following open ports. 
```bash
$ sudo nmap -p- --open -sS -sC -sV --min-rate 5000 -n -Pn -A 10.129.229.41 -oG tcp_scan.xml
```
-p- → Scans all 65,535 TCP ports, not just the most common ones. All 65,535 TCP ports, not just the most common ones, not just the most common ones. 

--open → Shows only ports that are open, filtering out closed or filtered ones.

-sS → Performs a TCP SYN scan (half-open scan), which is fast and stealthy and requires root privileges.

-sC → Runs default NSE (Nmap Scripting Engine) scripts to gather additional information such as common vulnerabilities and service details.

-sV → Attempts to detect service versions running on open ports.

--min-rate 5000 → Forces Nmap to send at least 5000 packets per second, speeding up the scan but increasing the chance of detection or packet loss. 

-n →  Disables DNS resolution to make the scan faster.

-Pn → Skips host discovery and assumes the target is alive, useful when ICMP is blocked.

-A → Enables aggressive scan options, including OS detection, version detection, script scanning, and traceroute.

-oG → Output option: write results in XML format to file nmap.xml.  Other formats: -oN (normal), -oG (grepable), -oA (all formats).

![alt text](Images/Nmap.png)

First of all we will try to open with our browser the IP. To access the website, we must add the IP to our /etc/hosts file to resolve the connection with the IP address.
```bash
$ echo "10.129.229.41" | sudo tee -a /etc/hosts 
```
![alt text](Images/Host.png)

Now we can go to the website through the port 80

![alt text](Images/Browser.png)


When accessing the IP address on port 80 indicated by Nmap, we can observe the following screen displaying the message "To raise an IT support ticket, please visit tickets.keeper.htb/rt/"
If, while browsing the web, we go to the Wappalyzer application or run a WhatWeb scan in our command-line console, we will see that we do not obtain any additional information beyond what has already been provided by Nmap.
```bash
$ whatweb 10.129.229.41
```
![alt text](Images/Wappalyzer.png)

![alt text](Images/Whatweb.png)

We add this domain to our /etc/hosts file:
```bash
$ echo "10.129.229.41 tickets.keeper.htb" | sudo tee -a /etc/hosts
```

![alt text](Images/Hosts.png)

Once we access the website, we see a login panel.

![alt text](Images/Browser2.png)

A brief Google search for the default Request Tracker credentials takes us to the documentation, where it states that the username is root and the password is password.
```bash
User: root
Password: password
```

![alt text](Images/Browser3.png)

Using the default credentials, we successfully log in and are redirected to the Request Tracker dashboard.


[Back](README.md)
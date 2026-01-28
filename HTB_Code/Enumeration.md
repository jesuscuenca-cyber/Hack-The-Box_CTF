First of all we check that we have connection with IP target.
```bash
$ ping -c 1 10.129.231.240
```
![alt text](Images/Ping.png)

This TTL value on HTB indicates that is a Linux machine.

We will start with our usual Nmap scan and find the following open ports. 

```bash
$ sudo nmap -p- --open -sS -sC -sV --min-rate 5000 -n -Pn -A 10.129.231.240 -oX tcp_scan.xml
$ xsltproc tcp_scan.xml -o tcp_scan.html
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

-oX → Output option: write results in XML format to file nmap.xml.  Other formats: -oN (normal), -oG (grepable), -oA (all formats).

![alt text](Images/Nmap.png)

First of all we will try to open with our browser the IP. To access the website, we must add the IP to our /etc/hosts file to resolve the connection with the IP address.

```bash
$ echo "10.129.231.240" | sudo tee -a /etc/hosts 
```
![alt text](Images/Hosts.png)

Now we can go to the website through the port 5000

![alt text](Images/Browser.png)

It appears to be a web application where we can execute Python code directly from the browser. In this webpage we can see that we can register on the website, so let's do it.

![alt text](Images/Login.png)

Once registered, it seems that we can save our programmed code.

![alt text](Images/Login2.png)



[Back](README.md)
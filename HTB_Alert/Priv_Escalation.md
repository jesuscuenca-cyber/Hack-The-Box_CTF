By checking the open ports with `netstat`, a network utility that shows active connections and listening ports, we observe that port `8080` is listening locally.
```bash
$ netstat -tulnp
```
![alt text](Images/Netstat.png)

We can proceed to port forward the target's port 8080 back to our port 8080 via SSH to check its service.
```bash
$ ssh albert@alert.htb -L 8080:127.0.0.1:8080
```
![alt text](Images/SSH2.png)

Accessing the port, we come across a Website Monitor page.

![alt text](Images/Browser2.png)

Let's browse until we find out where the ‘website monitor’ is.

![alt text](Images/Location.png)

![alt text](Images/Permisions.png)

We see that the vast majority of elements are owned by root.

Knowing that the web service operates with PHP and that I have write permissions in ‘monitors’ with my current credentials, we can do the following:
```bash
$ nano test.php

$ <?php system("whoami && id"); ?>
```
![alt text](Images/TestPHP.png)

And now we go to our browser  → http://localhost:8080/monitors/test.php

![alt text](Images/Ans_TestPHP.png)

We are root becasue we will execute commands as a root (service propietary) so with this, we are going to give suid permission to bash.

![alt text](Images/Permisions2.png)

We edit our test.php file like

![alt text](Images/TestPHP2.png)

Save the file and go to the previous link to our browser ( http://localhost:8080/monitors/test.php), this comand should have been executed.

![alt text](Images/Browser3.png)

![alt text](Images/Chmod.png)


Now we have permision as SUID, so if we do
```bash
$ bash -p
```
We will be root

![alt text](Images/Root_Flag.png)
```bash
Root Flag → 9c1833f971887a8e7a480715c909ac43
```

[Back](README.md)
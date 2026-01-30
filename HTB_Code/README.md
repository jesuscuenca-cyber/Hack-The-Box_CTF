![alt text](Images/Code.png)

# Scope

**Code** is a beginner-friendly Linux machine that hosts a web-based Python code editor vulnerable to **remote code execution** through a Python jail escape. By exploiting this flaw, an attacker can gain access as the **appproduction** user.
Once inside, weak credentials are discovered in an **SQLite3 database**, which can then be used to log in as another user, **martin**. This account has **sudo privileges** over a backup script called **backy.sh**.
The script contains insecure logic that can be abused to perform a **privilege escalation**, ultimately allowing the attacker to create a copy of the root directory and gain full system control.

# Index
- [Enumeration](Enumeration.md)
- [Foothold](Foothold.md)
- [Lateral Movement](Lateral_Movement.md)
- [Priv Escalation](Priv_Escalation.md)


Go back to [Hack-The-Box_CTF](https://github.com/jesuscuenca-cyber/Hack-The-Box_CTF)
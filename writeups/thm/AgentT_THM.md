# Agent T - TryHackMe Writeup

**Challenge Link:** [Agent T @ TryHackMe](https://tryhackme.com/room/agentt)  
**Difficulty:** Easy  
**Category:** Web, Exploitation  
**Platform:** TryHackMe

---

## 1. Initial Enumeration

Start with an **nmap** scan to discover open ports and services:

```bash
nmap -sV 10.10.18.111
```
**Options Breakdown:**  
- `-sV`: Service/version detection

**Result:**  
Only port 80 (HTTP) is open.  
![Nmap scan result](/img/writeups/AgentT/image.png)

The server is running **PHP 8.1.0-dev** (important for later).

---

## 2. Web Service Investigation

Access the web page via HTTP:

```
http://10.10.18.111/
```

![Homepage](/img/writeups/AgentT/image-1.png)

There is an **admin panel**, but none of the buttons work.

---

## 3. Vulnerability Research

Check [ExploitDB](https://www.exploit-db.com) for vulnerabilities related to **PHP 8.1.0-dev**.

Found an exploit for this version:  
![ExploitDB result](/img/writeups/AgentT/image-4.png)

---

## 4. Exploitation

Download the exploit (from ExploitDB) and run it:

```bash
python3 exploit.py
```

![Exploit running](/img/writeups/AgentT/image-5.png)

A shell is obtained! 🥳  
![Shell screenshot](/img/writeups/AgentT/image-6.png)

Check privileges:

```bash
whoami
```
Result: `root` (critical misconfiguration).

---

## 5. Capture the Flag

Find the flag file:

```bash
find / -name flag.txt
```

![Flag found](/img/writeups/AgentT/image-9.png)

---

## 6. Conclusion

- Enumerated open ports with nmap.
- Discovered PHP version and researched vulnerabilities.
- Used a public exploit to gain root shell.
- Located and captured the flag.

---

## Tips

- Always check service versions for known exploits.
- Use ExploitDB and similar resources for quick vulnerability research.

---

## Final Thoughts

GG! 🎉 Challenge completed.  
You enumerated, exploited, and captured the flag.  
Great job, Agent!
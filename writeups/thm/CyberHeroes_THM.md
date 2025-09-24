# CyberHeroes - TryHackMe Writeup

**Challenge Link:** [CyberHeroes @ TryHackMe](https://tryhackme.com/room/cyberheroes)  
**Difficulty:** Easy  
**Category:** Web, Enumeration  
**Platform:** TryHackMe

## 1. Initial Enumeration

Let's start with an **nmap** scan to discover open ports and services:

```bash
nmap -sV [IP_ADDRESS]
```
**Options Breakdown:**  
- `-sV`: Service/version detection

**Result:**  
Ports 22 (SSH) and 80 (HTTP) are open.
![Nmap scan result](/img/writeups/CyberHeroes/nmap.png)

---

## 2. Web Service Investigation

### Accessing the Web Page

First, try accessing the site via HTTP:

```
http://[IP_ADDRESS]:80/
```

![Homepage](/img/writeups/CyberHeroes/Homepage.png)

The homepage has links to **Home**, **About**, and **Login**.

---

### About Page

The About page is just a scroll of the homepage. Nothing interesting here.

---

## 3. Directory Brute-Forcing

Use **gobuster** to look for hidden directories:

```bash
gobuster dir -u http://[IP_ADDRESS]/ -w /usr/share/wordlists/Seclists/Discovery/Web-Content/raft-small-directories.txt
```
**Options Breakdown:**  
- `dir`: Directory brute-force mode  
- `-u`: Target URL  
- `-w`: Wordlist file

![Gobuster screenshot](/img/writeups/CyberHeroes/Gobuster.png)
*Result: /assets can be accessed.* 
Accessing `/assets` reveals some images and CSS files, but nothing useful for our goal. 

---

## 4. Login Page Analysis

Inspect the login page's source code. We find the following JavaScript:

```js
<script>
    function authenticate() {
      a = document.getElementById('uname')
      b = document.getElementById('pass')
      const RevereString = str => [...str].reverse().join('');
      if (a.value=="h3ck3rBoi" & b.value==RevereString("54321@terceSrepuS")) { 
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            document.getElementById("flag").innerHTML = this.responseText ;
            document.getElementById("todel").innerHTML = "";
            document.getElementById("rm").remove() ;
          }
        };
        xhttp.open("GET", "RandomLo0o0o0o0o0o0o0o0o0o0gpath12345_Flag_"+a.value+"_"+b.value+".txt", true);
        xhttp.send();
      }
      else {
        alert("Incorrect Password, try again.. you got this hacker !")
      }
    }
</script>
```

#### Credential Discovery

Analyze the logic:

```js
const RevereString = str => [...str].reverse().join('');
if (a.value=="h3ck3rBoi" & b.value==RevereString("54321@terceSrepuS")) { 
```

- **Username:** `h3ck3rBoi`
- **Password:** Reverse of `54321@terceSrepuS` → `SuperSecret@12345`

---

## 5. Getting the Flag

Login with the discovered credentials:

- **Username:** `h3ck3rBoi`
- **Password:** `SuperSecret@12345`

🎉 Upon successful login, the flag is revealed!

---

## 6. Conclusion

- Enumerated open ports with nmap.
- Explored the web service and brute-forced directories.
- Inspected JavaScript to find hardcoded credentials.
- Logged in and captured the flag.

---

## Tips

- Always inspect client-side code for clues.
- Use tools like nmap and gobuster for enumeration.
- Try both HTTP and HTTPS if one fails.

---

## Final Thoughts

GG! 🎉 You did it—challenge completed!  
You enumerated, investigated, cracked the credentials, and captured the flag.  
Great job, CyberHero!

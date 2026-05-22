---
title: "Example Writeup - TryHackMe Challenge"
date: 2026-05-22
category: TryHackMe
difficulty: Easy
tags: [TryHackMe, CTF, Web]
status: draft
description: "Step-by-step solution to a TryHackMe challenge"
---

# TryHackMe Challenge Writeup

## Challenge Details
**Platform:** TryHackMe  
**Difficulty:** Easy  
**Category:** Web  

## Approach

### Step 1: Reconnaissance
First, let me gather information about the target.

```bash
# Perform network reconnaissance
nmap -sV -sC target
```

### Step 2: Vulnerability Discovery
Scan for common vulnerabilities.

```bash
# Check for web vulnerabilities
nikto -h target
```

## Solution

### Finding the Flag

1. Explore the web application
2. Identify the vulnerability
3. Exploit and capture the flag

Add images of your progress:

```markdown
![Step 1 screenshot](./images/step1.png)
```

## Key Learnings

- What did you learn from this challenge?
- What techniques did you practice?

## References

- [OWASP](https://owasp.org)
- [TryHackMe](https://tryhackme.com)

---

**Next Steps:** After completing this template, rename the file (remove "DRAFT" from filename), add your content, and push to publish!

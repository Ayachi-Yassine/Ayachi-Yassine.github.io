---
layout: default
title: Certifications & Credentials
permalink: /certifications/
---

<style>
    .cert-card {
        background-color: var(--bg-secondary);
        border: 1px solid var(--border-color);
        border-radius: var(--radius-lg);
        padding: var(--spacing-lg);
        margin-bottom: var(--spacing-lg);
        transition: all var(--transition-base);
    }
    
    .cert-card:hover {
        border-color: var(--accent-primary);
        box-shadow: var(--shadow-lg);
    }
    
    .cert-icon {
        font-size: 2em;
        margin-right: var(--spacing-md);
        display: inline-block;
    }
    
    .cert-header {
        display: flex;
        align-items: center;
        margin-bottom: var(--spacing-md);
    }
    
    .cert-name {
        font-size: var(--font-size-lg);
        font-weight: var(--font-weight-bold);
        color: var(--accent-secondary);
        margin: 0;
    }
    
    .cert-status {
        display: inline-block;
        padding: var(--spacing-xs) var(--spacing-md);
        border-radius: 20px;
        font-size: var(--font-size-sm);
        margin-top: var(--spacing-md);
    }
    
    .status-in-progress {
        background-color: rgba(210, 153, 34, 0.1);
        color: var(--accent-warning);
        border: 1px solid rgba(210, 153, 34, 0.3);
    }
    
    .status-active {
        background-color: rgba(63, 185, 80, 0.1);
        color: var(--accent-success);
        border: 1px solid rgba(63, 185, 80, 0.3);
    }
    
    .status-completed {
        background-color: rgba(88, 166, 255, 0.1);
        color: var(--accent-primary);
        border: 1px solid rgba(88, 166, 255, 0.3);
    }
    
    .roadmap-section {
        background-color: var(--bg-secondary);
        border-left: 4px solid var(--accent-primary);
        padding: var(--spacing-lg);
        margin: var(--spacing-lg) 0;
        border-radius: var(--radius-md);
    }
    
    .roadmap-section h3 {
        color: var(--accent-secondary);
        margin-top: 0;
    }
    
    .checklist {
        list-style: none;
        padding-left: 0;
    }
    
    .checklist li {
        padding: var(--spacing-sm) 0;
        padding-left: var(--spacing-lg);
        position: relative;
        color: var(--text-primary);
    }
    
    .checklist li:before {
        content: "☐";
        position: absolute;
        left: 0;
        color: var(--accent-primary);
        font-weight: bold;
        font-size: var(--font-size-lg);
    }
    
    .learning-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: var(--spacing-lg);
        margin: var(--spacing-xl) 0;
    }
</style>

# 📜 Certifications & Learning Path

<p style="font-size: var(--font-size-lg); color: var(--text-secondary); margin-bottom: var(--spacing-xl);">
    Track my security certifications, learning progress, and professional development in cybersecurity.
</p>

## Active Certifications

<div class="cert-card">
    <div class="cert-header">
        <span class="cert-icon">🎓</span>
        <h3 class="cert-name">eJPT (eLearningSecurity Junior Penetration Tester)</h3>
    </div>
    <span class="cert-status status-in-progress">In Progress</span>
    
    <h4 style="margin-top: var(--spacing-lg); color: var(--accent-secondary);">Focus Areas</h4>
    <ul>
        <li>Network fundamentals</li>
        <li>Footprinting and scanning</li>
        <li>Enumeration techniques</li>
        <li>Exploitation basics</li>
        <li>Professional reporting</li>
    </ul>
</div>

<div class="cert-card">
    <div class="cert-header">
        <span class="cert-icon">🎮</span>
        <h3 class="cert-name">TryHackMe</h3>
    </div>
    <span class="cert-status status-active">Active</span>
    
    <p>Building practical skills through CTF challenges and security exercises.</p>
    
    <h4 style="margin-top: var(--spacing-lg); color: var(--accent-secondary);">Covered Topics</h4>
    <ul>
        <li>Linux fundamentals</li>
        <li>Web application security</li>
        <li>Network security</li>
        <li>Penetration testing basics</li>
        <li>Privilege escalation</li>
    </ul>
</div>

---

## 2026 Learning Roadmap

<div class="learning-grid">
    <div class="roadmap-section">
        <h3>Q1 - Foundation Building</h3>
        <ul class="checklist">
            <li>Complete eJPT certification</li>
            <li>Master Nmap and Burp Suite</li>
            <li>50+ TryHackMe rooms</li>
            <li>Network fundamentals deep dive</li>
            <li>First penetration test report</li>
        </ul>
    </div>
    
    <div class="roadmap-section">
        <h3>Q2 - Advanced Topics</h3>
        <ul class="checklist">
            <li>OSCP preparation</li>
            <li>Advanced exploitation techniques</li>
            <li>Web app security deep dive</li>
            <li>API security testing</li>
            <li>3+ security projects</li>
        </ul>
    </div>
    
    <div class="roadmap-section">
        <h3>Q3 - Specialization</h3>
        <ul class="checklist">
            <li>Choose specialization path</li>
            <li>Hands-on lab setup</li>
            <li>Real-world scenario practice</li>
            <li>Vulnerability research</li>
            <li>Custom tool development</li>
        </ul>
    </div>
    
    <div class="roadmap-section">
        <h3>Q4 - Certification Push</h3>
        <ul class="checklist">
            <li>Target additional certifications</li>
            <li>Complete portfolio projects</li>
            <li>Public CTF participation</li>
            <li>Blog post writing (5+)</li>
            <li>Open source contributions</li>
        </ul>
    </div>
</div>

---

## Quick Tips

<div style="background-color: rgba(88, 166, 255, 0.05); border-left: 4px solid var(--accent-primary); padding: var(--spacing-lg); border-radius: var(--radius-md); margin: var(--spacing-xl) 0;">
    <h3 style="margin-top: 0; color: var(--accent-secondary);">💡 Update This Page</h3>
    <p>
        Keep track of your certifications and progress here! Edit <code>certifications/index.md</code> to update your status.
    </p>
    <p style="font-size: var(--font-size-sm); margin: var(--spacing-md) 0 0 0; color: var(--text-secondary);">
        For detailed instructions on editing and publishing content, see the <a href="{{ '/LOCAL_EDITING_GUIDE.md' | relative_url }}">📚 Local Editing Guide</a>.
    </p>
</div>

---

## 🛠️ Current Tools & Skills

### Penetration Testing
- Nmap
- Burp Suite
- Metasploit Framework
- Wireshark

### Programming
- Python (scripting & automation)
- Bash (shell scripting)
- JavaScript (web vulnerabilities)

### Operating Systems
- Linux (Kali, Ubuntu)
- Windows (security concepts)

---

## 📚 Resources & References

- [eLearningSecurity Academy](https://elearnsecurity.com/)
- [TryHackMe Platform](https://tryhackme.com/)
- [OWASP Top 10](https://owasp.org/)
- [HackTheBox](https://www.hackthebox.com/)

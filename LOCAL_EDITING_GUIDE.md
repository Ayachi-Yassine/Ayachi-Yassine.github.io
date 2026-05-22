# Local Editing Guide 📚

Welcome! This guide will help you work on your portfolio locally, edit content offline, and publish to your GitHub Pages site when ready.

## Table of Contents
1. [Quick Start](#quick-start)
2. [Project Structure](#project-structure)
3. [Creating & Editing Content](#creating--editing-content)
4. [Adding Images](#adding-images)
5. [Draft vs Published](#draft-vs-published)
6. [Front Matter Reference](#front-matter-reference)
7. [Local Preview](#local-preview)
8. [Publishing](#publishing)
9. [Recommended Tools](#recommended-tools)

---

## Quick Start

### Prerequisites
- **Ruby** (version 2.7+) — [Install here](https://www.ruby-lang.org/en/downloads/)
- **Git** — [Install here](https://git-scm.com/)
- A code editor (VS Code, Sublime, Obsidian, etc.)

### First Time Setup

```bash
# Navigate to your project folder
cd ~/Desktop/github/Ayachi-Yassine.github.io

# Install dependencies (one time only)
gem install bundler
bundle install

# Start the local development server
bundle exec jekyll serve

# Open in browser: http://localhost:4000
```

**That's it!** Your site is now running locally. Any changes you make to files will automatically refresh in the browser.

---

## Project Structure

```
Ayachi-Yassine.github.io/
├── index.html                 # Landing page
├── assets/
│   └── css/                  # Styling (theme.css, components.css, responsive.css)
├── _layouts/
│   └── default.html          # Main page template
├── _data/
│   └── site.yml              # Site metadata, navigation, skills
├── _projects/                # ✍️ Create pentesting projects here
├── _writeups/                # ✍️ Create CTF writeups here
├── _research/                # ✍️ Create research papers here
├── projects/
│   └── index.html            # Browses all projects
├── writeups/
│   └── index.html            # Browses all writeups
├── research/
│   └── index.html            # Browses all research
├── certifications/
│   └── index.md              # Certifications page
└── _config.yml               # Jekyll configuration
```

**Key folders for editing:**
- `_projects/` — Add pentesting reports and security assessments
- `_writeups/` — Add CTF solutions and challenge walkthroughs
- `_research/` — Add CVE analysis and security research papers

---

## Creating & Editing Content

### Create a New Project/Writeup/Research File

**Filename pattern:** `_writeups/YYYY-MM-DD-title.md` or `_writeups/YYYY-MM-DD-DRAFT-title.md`

**Example files location:**
```
_projects/2026-05-22-example-owasp-testing.md       # Example (published)
_writeups/2026-05-22-DRAFT-example-tryhackme.md    # Example (draft)
_research/2026-05-22-DRAFT-cve-analysis.md         # Example (draft)
```

### Template: Pentesting Project

Create a new file: `_projects/2026-06-01-my-project.md`

```markdown
---
title: "Project Title - Description"
date: 2026-06-01
category: Web           # [Web, Network, Cryptography, etc]
difficulty: Medium     # [Easy, Medium, Hard]
tags: [tag1, tag2]
status: published      # Change to "draft" if not ready
description: "Short description for the project card"
---

# Project Title

## Executive Summary
Brief overview of what this project covers.

## Objectives
- Objective 1
- Objective 2

## Tools Used
- Tool 1
- Tool 2

## Findings

### Finding #1
Description with images:

![Screenshot](./images/screenshot.png)

## Recommendations
- Recommendation 1
- Recommendation 2

## Conclusion
Final thoughts.
```

### Template: CTF Writeup

Create a new file: `_writeups/2026-06-01-my-writeup.md`

```markdown
---
title: "Challenge Name - Platform"
date: 2026-06-01
category: TryHackMe    # [TryHackMe, HackTheBox, PicoCTF, etc]
difficulty: Easy
tags: [Web, SQL, Authentication]
status: published
description: "Step-by-step walkthrough of the challenge"
---

# Challenge Writeup

## Challenge Info
- **Platform:** TryHackMe
- **Difficulty:** Easy
- **Category:** Web Application

## Approach

### Reconnaissance
```bash
# Your commands here
```

### Exploitation
Steps and screenshots:

![Step screenshot](./images/step1.png)

### Flag
`flag{captured_flag_here}`

## Lessons Learned
What did you learn?
```

### Template: Security Research

Create a new file: `_research/2026-06-01-my-research.md`

```markdown
---
title: "CVE-2026-XXXXX: Vulnerability Analysis"
date: 2026-06-01
category: CVE
tags: [CVE, Exploit, Research, Critical]
status: published
description: "Analysis of a critical security vulnerability"
---

# CVE-2026-XXXXX: Vulnerability Title

## Overview
Brief description of the vulnerability.

## Technical Details
- **CVSS Score:** 9.8
- **Affected Software:** [Product v1.0-v2.5]
- **Vulnerability Type:** [RCE, SQL Injection, etc]

## Root Cause Analysis
Explain the vulnerability.

## Proof of Concept
```python
# PoC code
```

## Impact & Mitigation
- Impact assessment
- Mitigation steps
```

---

## Adding Images

### File Structure with Images

Keep images alongside your content:

```
_projects/
├── 2026-06-01-my-project.md
└── 2026-06-01-my-project/
    └── images/
        ├── screenshot1.png
        ├── screenshot2.jpg
        └── diagram.svg

_writeups/
├── 2026-06-01-my-writeup.md
└── 2026-06-01-my-writeup/
    └── images/
        ├── step1.png
        └── flag-screen.png
```

### Reference Images in Markdown

```markdown
# Simple image reference (relative path)
![Alt text for accessibility](./images/screenshot.png)

# With title
![Alt text](./images/screenshot.png "Screenshot Title")

# Size specification (if needed)
<img src="./images/screenshot.png" width="600" alt="Description">
```

### Workflow: Adding Images

1. **Create the images folder:**
   ```
   _projects/2026-06-01-my-project/images/
   ```

2. **Copy your images** directly into that folder

3. **Reference in markdown:**
   ```markdown
   ![My screenshot](./images/screenshot.png)
   ```

4. **Preview locally** with `jekyll serve` to verify images display

5. **Push to GitHub** when ready to publish

---

## Draft vs Published

### Making Content Private (Draft)

**Option 1: Use "draft" status**
```yaml
---
title: "My Project"
status: draft
---
```

**Option 2: Prefix filename with "DRAFT-"**
```
_projects/2026-06-01-DRAFT-my-project.md  # Won't appear on site
_projects/2026-06-01-my-project.md        # Published
```

### Publishing Draft Content

Simply remove the draft indicator:

```bash
# Rename the file (remove DRAFT- prefix or change status to published)
git mv "_projects/2026-06-01-DRAFT-my-project.md" "_projects/2026-06-01-my-project.md"

# Commit and push
git add .
git commit -m "Publish: My project writeup"
git push
```

---

## Front Matter Reference

Every file needs a header with metadata (YAML front matter):

```yaml
---
title: "Your Title Here"              # Required: Page title
date: YYYY-MM-DD                      # Required: Publication date
category: Web                         # Required: Category (Web, Network, CVE, etc)
difficulty: Medium                    # Optional: [Easy, Medium, Hard]
tags: [tag1, tag2, tag3]             # Optional: Array of tags for filtering
status: published                     # Optional: published or draft
description: "Short card description" # Optional: Shows on listing pages
---
```

### Category Values
- **Projects:** Web, Network, Cryptography, Reverse Engineering, Scripting
- **Writeups:** TryHackMe, HackTheBox, PicoCTF, CtfTime, Custom
- **Research:** CVE, Exploit, Vulnerability, Article

### Difficulty Values
- Easy
- Medium
- Hard
- Expert

---

## Local Preview

### Start the Development Server

```bash
# Navigate to project folder
cd ~/Desktop/github/Ayachi-Yassine.github.io

# Start Jekyll
bundle exec jekyll serve
```

### View Your Site

Open browser to: **`http://localhost:4000`**

### Live Reload
- Changes to `.md` files → Auto-refresh (just reload browser)
- Changes to `.css` files → Auto-refresh
- Changes to `_config.yml` → Need to restart (Ctrl+C, then `bundle exec jekyll serve` again)

---

## Publishing

### One-Time Git Setup

```bash
cd ~/Desktop/github/Ayachi-Yassine.github.io

# Configure git (if not done before)
git config user.name "Your Name"
git config user.email "your-email@example.com"
```

### Publish Your Work

```bash
# 1. Check what changed
git status

# 2. Add your changes
git add .

# 3. Commit with a message
git commit -m "Add: New project writeup - describe here"

# 4. Push to GitHub
git push origin main
```

### Verify Publication

After pushing, your site updates automatically:
- Visit: **`https://Ayachi-Yassine.github.io`**
- Changes appear in ~30 seconds to 1 minute

---

## Recommended Tools

### For Writing & Editing

#### Option 1: **Obsidian** (Notion-like, Recommended!)
- Works perfectly with your markdown structure
- Live preview as you type
- Folder browser matches your `_projects/`, `_writeups/` organization
- [Download Obsidian](https://obsidian.md)

**Setup:**
```
1. Open Obsidian
2. Create a vault pointing to: ~/Desktop/github/Ayachi-Yassine.github.io
3. Edit files directly in the folder view
4. See live preview on the right side
```

#### Option 2: **VS Code**
- Free and lightweight
- Good markdown preview
- Terminal integration for `jekyll serve`
- Recommended extensions:
  - Markdown All in One
  - Markdown Preview Enhanced
  - Jekyll Snippets

#### Option 3: **Any Text Editor**
- Sublime Text, Notepad++, atom, etc.
- Pair with `jekyll serve` in a terminal for live preview

### Command Line Tools

#### Check Local Site
```bash
# Navigate to folder
cd ~/Desktop/github/Ayachi-Yassine.github.io

# Start server
bundle exec jekyll serve

# Open http://localhost:4000 in browser
```

#### Git Commands Cheat Sheet
```bash
# See what changed
git status

# Add all changes
git add .

# Commit with message
git commit -m "Describe your changes"

# Push to GitHub
git push

# View commit history
git log --oneline

# Undo last commit (before push)
git reset HEAD~1
```

---

## Common Tasks

### Add a New Project

```bash
# 1. Create file
# _projects/2026-06-15-my-security-audit.md

# 2. Add content with template above

# 3. Create images folder (if needed)
# _projects/2026-06-15-my-security-audit/images/

# 4. Copy images to that folder

# 5. Reference in markdown
# ![screenshot](./images/audit-screenshot.png)

# 6. Test locally: http://localhost:4000/projects/

# 7. Commit and push
git add .
git commit -m "Add: Security audit project"
git push
```

### Edit an Existing Page

```bash
# 1. Edit _projects/existing-project.md

# 2. Save and preview at localhost:4000

# 3. Commit and push
git add .
git commit -m "Update: Fix typo in project description"
git push
```

### Move Draft to Published

```bash
# Option A: Change status in YAML
# From: status: draft
# To:   status: published

# Option B: Rename file (remove DRAFT-)
mv "_projects/2026-06-01-DRAFT-project.md" "_projects/2026-06-01-project.md"

# Commit
git add .
git commit -m "Publish: Project name"
git push
```

---

## Troubleshooting

### Port 4000 Already In Use
```bash
# Kill the process
# Mac/Linux:
lsof -i :4000
kill -9 <PID>

# Windows:
netstat -ano | findstr :4000
taskkill /PID <PID> /F
```

### Changes Not Showing
- Refresh browser (Ctrl+R or Cmd+R)
- If CSS changed, do a hard refresh (Ctrl+Shift+R)
- If `_config.yml` changed, restart jekyll (Ctrl+C, then run again)

### Images Not Showing
- Check path in markdown: should be `./images/filename.png` (relative path)
- Verify image file exists in the folder
- Check file extension matches (`.png`, `.jpg`, etc)
- Restart jekyll

### Git Push Fails
```bash
# Pull latest changes first
git pull origin main

# Then push
git push origin main
```

---

## Tips & Best Practices

### Markdown Tips
- Use `#` for headings (don't use h1 `#` in content — Jekyll handles that)
- Use triple backticks ` ``` ` for code blocks
- Add `bash`, `python`, `javascript` after backticks for syntax highlighting
- Images: `![description](./images/file.png)` not `![description](file.png)`

### Naming Tips
- Use lowercase and hyphens: `my-project`, not `My Project` or `my_project`
- Include dates: `2026-06-01-title.md`
- Keep filenames short but descriptive

### Content Tips
- Start with a compelling title and description
- Add a brief overview at the top of each writeup
- Include tools/technologies used
- Add screenshots/images to break up text
- End with key learnings or recommendations

### Performance Tips
- Optimize images before adding (1-2 MB max per image)
- Use `.jpg` for photos, `.png` for screenshots with text
- Avoid videos (use GIFs or screenshots instead)

---

## Need Help?

- **Jekyll Docs:** https://jekyllrb.com/docs/
- **Markdown Guide:** https://www.markdownguide.org/
- **GitHub Pages Docs:** https://docs.github.com/en/pages

---

## Next Steps

1. **Start writing!** Create your first writeup or project
2. **Test locally** with `jekyll serve`
3. **Preview** at http://localhost:4000
4. **Commit and push** when ready
5. **Celebrate!** Your portfolio is live 🚀

Happy writing! 🛡️

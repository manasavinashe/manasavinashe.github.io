# Add Project to Portfolio — Claude Prompt

Copy everything below the line and paste it into a Claude session running inside your project folder.

---

You are helping me add this project to my Astro portfolio site located at:
`/Users/manas/Documents/Astro_papaer/wretched-wavelength`

## Step 1 — Understand the Project

Explore this directory thoroughly. Read source files, notebooks, reports, and output folders. Understand:
- What the project does and why it was built
- The tech stack and methodology
- Concrete results and metrics

## Step 2 — Choose a Slug

Pick a short, descriptive, hyphenated slug for this project (e.g., `hybrid-cnn-framework`, `robo-advisor-risk`). You will use this slug as:
- The markdown filename
- The images subfolder name

## Step 3 — Collect Images

Find all output charts, figures, or result images in this project directory. Copy the most relevant ones to:
```
./portfolio_export/images/<slug>/
```
Only include images that directly support the writeup — skip raw data dumps or debug plots.

## Step 4 — Write the Markdown File

Save the file to `./portfolio_export/<slug>.md`.

### Frontmatter (required)

```yaml
---
title: "Catchy and Descriptive Project Title"
description: "A 1-2 sentence high-level summary of what the project does."
category: "computer-vision"  # MUST be exactly "finance" or "computer-vision"
pubDatetime: YYYY-MM-DDTHH:00:00Z
github: "https://github.com/manasavinashe/<repo-name>"  # fill in after Step 5
stack:
  - "Python"
  - "PyTorch"
  # list key technologies only
featured: true
---
```

### Body Layout

Write a professional portfolio writeup with these sections. Synthesise — do not copy-paste raw output.

- **## Overview** — What is this project and why was it built?
- **## The Problem** — What specific challenge does it solve?
- **## Methodology & Architecture** — Models, pipelines, algorithms. Embed images inline where relevant using: `![alt text](./images/<slug>/filename.png)`
- **## Results & Impact** — Concrete outcomes with metrics (accuracy, Sharpe, speed, etc.). Embed result charts here.

## Step 5 — GitHub Push Protocol

### 5a. Check and push the project repo

```bash
# Are we in a git repo?
git status

# Any unpushed commits?
git log --oneline origin/main..HEAD 2>/dev/null || echo "no remote"

# If uncommitted changes exist — commit them
git add -A
git commit -m "Final state: <brief description>"

# If no remote exists — stop here and note it
git remote -v

# If remote exists and there are unpushed commits — push
git push origin main

# Get the GitHub URL to put in the frontmatter github: field
git remote get-url origin
```

Update the `github:` field in the frontmatter with this URL, then re-save the markdown.

### 5b. Copy files into the portfolio site

```bash
# Copy the markdown file
cp ./portfolio_export/<slug>.md \
   /Users/manas/Documents/Astro_papaer/wretched-wavelength/src/data/projects/<slug>.md

# Copy the images subfolder
cp -r ./portfolio_export/images/<slug>/ \
   /Users/manas/Documents/Astro_papaer/wretched-wavelength/src/data/projects/images/<slug>/
```

### 5c. Commit and push the portfolio site

```bash
cd /Users/manas/Documents/Astro_papaer/wretched-wavelength

# Check what's new
git status

# Stage only the new project files
git add src/data/projects/<slug>.md src/data/projects/images/<slug>/

# Commit
git commit -m "Add <project title> project to portfolio"

# Push
git push origin main
```

## Step 6 — Report Back

When done, tell me:
1. The GitHub URL of this project repo (or "no remote" if none)
2. The portfolio site commit hash
3. The live path: `src/data/projects/<slug>.md`
4. Any images that were skipped and why

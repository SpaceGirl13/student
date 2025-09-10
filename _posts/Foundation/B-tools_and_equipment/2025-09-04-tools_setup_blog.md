---
title: "My Journey Setting Up Tools for My LxD Project"
date: 2025-09-09
author: Anishka Sanghvi
tags: ["tools", "setup", "vscode", "git", "learning-experience-design"]
---

# 🚀 My Journey Setting Up Tools for My Learning Experience Design Project

When I first started my project, I thought setting up the development environment would be quick and simple. In reality, it turned into one of my biggest learning experiences. Between the terminal, GitHub, virtual environments, and VS Code quirks, I had to troubleshoot quite a bit. 

Looking back, though, I'm glad it wasn't easy. Every challenge I faced gave me a clearer understanding of how developers *actually* work day-to-day.

---

## 🔧 What I Actually Learned During Installation

The setup process walked me through:

- Opening and navigating a **Linux/MacOS terminal** (scarier than I expected!)
- Managing **folders and files** with commands like `mkdir`, `ls`, and `cd`
- Cloning a **GitHub repo** and keeping it synced
- Installing and activating **tools and packages** like Ruby, Python, Git, and Homebrew
- Using VS Code with the `code .` command to connect everything together

This wasn't just about getting things to work — it was about understanding how all the pieces of the developer workflow actually fit together in real life.

---

## 🖼️ How I Visualized the Workflow

Here's how I started picturing the development process in my head:

1. 💻 **Terminal First** → I open my Mac terminal and run shell commands
2. 📁 **Clone a Project** → `git clone https://...` brings a repo from GitHub onto my laptop
3. 🛠️ **Activate Tools** → I set up Ruby, Python, Git, and my virtual environment
4. 🔄 **The Development Cycle** → edit code → test → `git commit` → `git push`

This helped me see how development is really a continuous loop, not a straight line from start to finish.

---

## 🐚 Commands That Became Second Nature

### Shell Commands (MacOS/Unix)
```bash
ls          # list files and folders
pwd         # show current directory path
mkdir       # create new folders
cd          # navigate between directories
cat         # read file content in terminal
```

### Version Control (Git)
```bash
git clone   # copy a repo from GitHub to my machine
git pull    # update my local copy with remote changes
git commit  # save my changes locally with a message
git push    # send my local changes to GitHub
```

### Package Manager (Homebrew)
```bash
brew list                    # see what's installed
brew search <package-name>   # find packages
brew update && brew upgrade  # keep everything fresh
brew uninstall <name>        # remove packages I don't need
```

These commands started feeling natural once I used them every day for a week.

---

## 🍎 My Step-by-Step MacOS Setup

### 1. Install Homebrew
I opened Terminal and followed the instructions from [brew.sh](https://brew.sh/). The command looked intimidating at first, but it worked perfectly.

### 2. Install VS Code Properly
- Downloaded it from Microsoft's official website
- **Important:** Dragged it into `/Applications` folder (not just Downloads!)
- This prevented the AppTranslocation issues I ran into later

### 3. First-Time Repository Setup
```bash
mkdir opencs
cd opencs
git clone https://github.com/Open-Coding-Society/student.git
cd student/
./scripts/activate_macos.sh
./scripts/activate.sh    # This asked for my Git username and email
./scripts/venv.sh
```

---

## ✅ Health Checks I Run Regularly

Whenever I want to verify everything is working correctly:

```bash
python --version
pip --version
ruby -v
bundle -v
gem --version
git config --global --list
```

If any of these fail or show unexpected versions, I know something needs fixing.

---

## 🏃‍♂️ My Daily Startup Routine

Every time I start a new coding session:

```bash
cd opencs/student
source venv/bin/activate    # Activate my Python virtual environment
code .                      # Open VS Code in current directory
```

---

## ⚠️ Real Problems I Faced (And Actually Solved)

### 1. VS Code Couldn't Find My Virtual Environment
**What happened:** VS Code kept using the system Python instead of my project's virtual environment.

**My debugging process:**
- Checked if `venv/bin/activate` was working in terminal ✅
- Looked at VS Code's Python interpreter setting ❌
- Noticed VS Code wasn't picking up the environment automatically

**The fix:** I cleared VS Code's workspace settings and relaunched it by running `code .` directly from the terminal while the virtual environment was active.

**Why it worked:** VS Code reads environment variables from the shell that launched it. When I activated the venv first, then opened VS Code, it inherited those settings.

### 2. The `code` Command Pointed to the Wrong Location
**What happened:** Running `code .` opened VS Code, but from a weird temporary folder path (something like `/private/var/folders/...AppTranslocation...`).

**My debugging process:**
- Ran `which code` to see where the command pointed
- Discovered it was pointing to a temporary macOS security folder, not the real app
- Realized this happens when apps aren't "properly" installed

**The fix:** 
```bash
# Remove the bad symlink
sudo rm /usr/local/bin/code

# Create a proper symlink to the real app location
sudo ln -s "/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code" /usr/local/bin/code
```

**Why it worked:** macOS's AppTranslocation security feature moves apps to temporary folders if it doesn't trust them. By installing VS Code properly in `/Applications` and creating the correct symlink, I bypassed this issue.

### 3. Git Credentials Kept Getting Lost
**What happened:** I had to enter my GitHub username and password every time I pushed code.

**My debugging process:**
- Realized I was using HTTPS instead of SSH for my repo
- GitHub had deprecated password authentication anyway

**The fix:** Set up SSH keys for GitHub authentication following their official guide. Now `git push` works seamlessly.

---

## 💡 What I'd Tell My Past Self

1. **Don't skip the "boring" setup steps** — they prevent hours of debugging later
2. **Learn the commands gradually** — you don't need to memorize everything at once
3. **Keep notes of what breaks** — you'll face similar issues again
4. **Use the terminal more** — VS Code's integrated terminal is your friend
5. **When something breaks, try to understand why** — not just how to fix it

---

## 🔄 My Current Workflow

Now that everything is set up properly, my development cycle looks like:

1. `cd opencs/student && source venv/bin/activate`
2. `git pull` to get latest changes
3. `code .` to open VS Code
4. Make changes, test them
5. `git add .`, `git commit -m "description"`, `git push`

It feels smooth and natural now, but getting here definitely took some persistence and troubleshooting skills I didn't know I had!
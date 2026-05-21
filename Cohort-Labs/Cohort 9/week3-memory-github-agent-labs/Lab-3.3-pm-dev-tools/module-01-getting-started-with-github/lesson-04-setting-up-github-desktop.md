# Lesson 04 · Setting Up GitHub Desktop

## What is GitHub Desktop?

GitHub Desktop is a **free, official desktop app made by GitHub** that gives you a visual interface to manage all your Git operations — without ever touching the terminal.

Every action you'd normally type as a command (`git clone`, `git commit`, `git push`, `git pull`) becomes a button click. You can see your changes visually, switch branches, and sync with GitHub — all from one clean window.

---

## GitHub Desktop vs Other Ways to Use GitHub

There are three main ways people interact with GitHub. Here's how they compare:

| | GitHub Website | Terminal (Git CLI) | GitHub Desktop |
|---|---|---|---|
| **What it is** | Browser-based UI at github.com | Command-line tool, type every command | Desktop app, visual interface |
| **Best for** | Browsing repos, reviewing PRs, reading code | Advanced users, full control, scripting | Beginners & everyday workflows |
| **Learning curve** | Low — just a website | High — must memorize commands | Low — point and click |
| **See file changes** | Yes, on the website | Yes, but text-only in terminal | Yes, visual side-by-side diff |
| **Works offline** | ❌ Needs browser + internet | ✅ Git works locally | ✅ App works locally |
| **Cloning a repo** | Copy URL, paste in terminal | `git clone <url>` | Click "Clone Repository" |
| **Speed for beginners** | Medium | Slow (lots to learn) | Fast |

> **Bottom line:** GitHub Desktop is the fastest way to go from zero to productive. Once you're comfortable, you can layer in terminal commands — but Desktop handles 95% of what you'll need day-to-day.

---

## Phase 2 · Installing & Setting Up GitHub Desktop

### Step 1 — Download GitHub Desktop

Go to **[https://github.com/apps/desktop](https://github.com/apps/desktop)** and click the **"Download Now"** button.

This is the official download page maintained by GitHub — you're getting the real, verified app directly from the source.

![Download GitHub Desktop](images/5.png)

---

### Step 2 — Choose the Right Version for Your Mac

After clicking download, you'll be asked to select your chip type:

- **Apple Silicon** → if your Mac was made in late 2020 or newer (M1, M2, M3, M4 chip)
- **Intel Chip** → if your Mac was made before 2020

> Not sure which one you have? Click the Apple  menu in the top-left corner of your screen → **"About This Mac"** → look under Chip or Processor.

![Select Mac Version](images/5.png)

---

### Step 3 — Open GitHub Desktop from Finder

Once the download completes:

1. Open **Finder** (the smiley face icon in your dock)
2. Type **"GitHub Desktop"** in the search bar (top right of Finder)
3. Double-click the app to open it

The app may ask if you want to move it to your Applications folder — click **Move to Applications**. This keeps your Mac organized and makes the app easy to find later.

![Open from Finder](images/6.png)

---

### Step 4 — Sign In with GitHub

When GitHub Desktop opens for the first time, you'll see a welcome screen.

Click **"Sign in to GitHub.com"**

This connects the desktop app to your GitHub account so it knows who you are, which repos you have access to, and where to push your code.

![Sign In to GitHub](images/7.png)

---

### Step 5 — Authorize the App and Finish Setup

Your browser will open automatically and ask you to **authorize GitHub Desktop**.

1. Click **"Authorize desktop"** — this gives the app permission to act on your behalf (clone, push, pull)
![Authorize GitHub Desktop](images/8.png)

2. Your browser will redirect back to the desktop app automatically
![Authorize GitHub Desktop](images/9.png)

3. Click **"Finish"** to complete the setup
![Authorize GitHub Desktop](images/10.png)

> This authorization is secure — GitHub uses OAuth, the same standard used by "Login with Google" buttons across the web.

---

### Step 6 — Select the Repo You Want to Clone

Now you'll see your GitHub repositories listed inside the app.

Find and select **`mahesh_aipmwebsite`** from the list.

> **What is cloning?** Cloning means downloading a full copy of the repository — all files, all folders, and the entire history of every change ever made — from GitHub's servers to your local machine. You're not just downloading files; you're downloading the full project with all its version history intact.

![Select Repository](images/6.png)

---

### Step 7 — Choose Where to Save the Repo on Your Computer

Before cloning, GitHub Desktop will ask you which repo you nmeed to clone clone the ai-community-site 

![Choose Clone Path](images/11.png)

Recommended: create a dedicated folder like `~/Documents/Projects/` or `~/Desktop/Dev/` and always clone your repos there. Keeping all your repos in one place makes them easy to find and manage.

Click **"choose"** once you've selected your path.

![Choose Clone Path](images/14.png)

---

### Step 8 — Your Repo is Cloned Successfully

GitHub Desktop will download the entire repository to your chosen folder. Once done, you'll see the repo name in the top-left of the app, with all your branches and recent commits visible.

You can now:
- **Open the repo in VS Code** by clicking "Open in Visual Studio Code"
- **See file changes** in the Changes tab as you edit files
- **Commit and push** your work back to GitHub with two clicks

> ✅ **Your repo is now cloned to your device through GitHub Desktop.** Every file is on your machine and ready to edit.

![Repo Cloned Successfully](images/13.png)

---

## What You Learned in This Lesson

| Concept | What It Means |
|---|---|
| **GitHub Desktop** | A visual app that replaces terminal Git commands with buttons and diffs |
| **Cloning** | Downloading the full repository — all files and all history — to your local machine |
| **Local vs Remote** | The "remote" is on GitHub's servers; the "local" is on your machine — they sync via push/pull |
| **Authorization** | GitHub uses OAuth to securely connect the desktop app to your account |

---

## Next Lesson

Your repo is on your machine. Now you need the tools to open it, read it, and run AI inside it.

**[→ Module 02, Lesson 01: Installing Node.js and VS Code](../module-02-installing-vscode-and-claude-code/lesson-01-installation.md)**

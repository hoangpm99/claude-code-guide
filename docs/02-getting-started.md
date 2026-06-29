# Getting Started

The goal of this page is simple: get you from a fresh machine to a **ready-to-work environment** — your IDE open with Claude Code running in the terminal, waiting for your first prompt.

There are two things to install.

## 1. Install an IDE: VS Code or Cursor

We'll use a code editor with a built-in terminal to run Claude Code. Pick one:

- **[Visual Studio Code](https://code.visualstudio.com/)** — free, the most common choice.
- **[Cursor](https://cursor.com/)** — a VS Code fork with extra AI features built in.

Either works. If you're unsure, go with VS Code.

## 2. Install Claude Code

On Windows, the smoothest path is to install Claude Code inside **WSL** (Windows Subsystem for Linux). I found this guide excellent and followed it end to end:

➡️ **[Installing Claude Code on Windows using WSL](https://www.ge-lab.org/2025/12/06/installing-claude-code-on-windows-using-wsl/)**

Rather than repeat it, here's what it walks you through and what you'll end up with.

**What it installs:**

- **WSL** + **Ubuntu** — a Linux environment running inside Windows.
- **nvm** and **Node.js** — Claude Code runs on Node.
- **Claude Code** itself (the CLI).

**The steps, in order:**

1. Check that virtualization is enabled, then run `wsl --install` from an Administrator PowerShell.
2. Restart, and finish Ubuntu setup (pick a username and password).
3. Update Ubuntu's packages.
4. Install Node.js via nvm.
5. Install Claude Code.
6. Sign in — with a Claude Pro/Max subscription or a Console API key.
7. Run `claude` to confirm it works.

> **Note:** signing in needs a Claude **Pro** or **Max** plan, or a **Console API key**. A subscription gives you both *Claude* (the chat app) and *Claude Code*. See [Use Claude Code with your Pro or Max plan](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-or-max-plan) for the details.

**The outcome:** you can open your project in VS Code (or Cursor), open the integrated terminal, type `claude`, and you're in.

## You're ready — start prompting

That's it. With Claude Code running in the terminal, you can now just *describe what you want* in plain language — "add a login page", "fix this failing test", "explain what this file does" — and watch Claude Code read your code, make changes, and run commands for you.

From here, the rest of this guide is about doing that *well*. Head to the [Workflow](03-workflow.md) page to see how I take a project from a rough idea to a shipped product.

## Skills

A **skill** is a reusable instruction set you can trigger with `/skill-name` (or that Claude runs automatically when relevant). It's just a folder with a `SKILL.md` file inside. They're how you teach Claude Code a repeatable procedure once instead of re-typing it every session — the whole workflow on the next page leans on them.

Skills live in one of two places:

- `~/.claude/skills/` (or `C:\Users\<YOUR_USERNAME>\.claude\skills` for Windows) — available in **every** project.
- `.claude/skills/` — only in **this** project (commit it to share with your team).

To add one, drop its folder in either location and Claude Code picks it up automatically. The [Workflow](03-workflow.md#setup-install-the-skills) page shows how to install a ready-made set.

➡️ Official reference: **[Extend Claude with skills](https://code.claude.com/docs/en/skills)**.

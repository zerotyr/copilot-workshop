# 02 — GitHub Copilot CLI

**Goal:** Use the GitHub Copilot CLI to work with an AI coding agent directly in your terminal — no context switching to a browser or editor required.

**Time:** ~10 minutes

---

## What Is the GitHub Copilot CLI?

The GitHub Copilot CLI is a standalone terminal tool that brings the same agentic Copilot coding assistant you use in VS Code directly to your command line. It can:

- Build, edit, debug, and refactor code through natural language conversation
- Read your local codebase and understand context the same way Copilot does in the editor
- Access your GitHub repositories, issues, and pull requests using your existing account
- Preview every action before executing — nothing happens without your approval

It's not a command lookup tool — it's a full agentic coding collaborator that lives in your terminal.

---

## Installation

Choose the method that works for your platform:

**macOS / Linux — install script:**
```sh
curl -fsSL https://gh.io/copilot-install | bash
```

**macOS / Linux — Homebrew:**
```sh
brew install copilot-cli
```

**Windows — WinGet:**
```sh
winget install GitHub.Copilot
```

**All platforms — npm:**
```sh
npm install -g @github/copilot
```

> **Prerequisite:** An active GitHub Copilot subscription is required.

---

## Getting Started

Launch the CLI from any directory:

```sh
copilot
```

On first launch you'll be prompted to authenticate with your GitHub account. Follow the on-screen instructions.

Launch it in a project folder — this gives it access to your codebase as context:

```sh
cd your-project
copilot
```

---

## Using the CLI

Once launched, you interact with Copilot conversationally. Type a task in plain English and it will plan and execute steps, asking for your approval before taking actions.

**Sample tasks to try in your project:**

```
Explain how authentication works in this codebase.
```

```
Find all the places where we're making database calls directly in a
controller and list them.
```

```
Add error handling to the function that processes user input. Run the
tests after to confirm nothing broke.
```

```
I'm getting a null pointer error in the payment service when the
order has no items. Find the cause and fix it.
```

```
Write a script that watches for changes to the src folder and runs
the tests automatically.
```

---

## Key Features

**Autopilot mode:** Press `Shift+Tab` to cycle into Autopilot mode, where Copilot continues working through a task until it's complete — not just one step at a time.

**Model selection:** Default model is Claude Sonnet 4.5. Use the `/model` slash command to switch to other available models.

**Slash commands:**

| Command | What it does |
|---|---|
| `/login` | Authenticate with GitHub |
| `/model` | Switch the active model |
| `/feedback` | Submit a confidential feedback survey |
| `/lsp` | View configured LSP servers |
| `/experimental` | Enable experimental features |

---

## Exercise

1. Open a terminal and navigate to your project from the Getting Started exercise
2. Launch `copilot`
3. Ask it to explain the structure of your project in plain English
4. Then give it a real task: ask it to find something, fix something, or add something small
5. Watch how it previews its planned actions before executing

---

## Reflection Questions

- How is this different from using Copilot Chat inside VS Code?
- Did it show you its plan before making changes? Did you approve or modify it?
- What kinds of tasks feel more natural to do in the terminal vs. in the editor?
- When would Autopilot mode be useful vs. stepping through actions manually?

---

## What's Next?

[03 — Context Engineering](../03-context-engineering/README.md)

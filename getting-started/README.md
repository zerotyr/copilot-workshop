# Getting Started

**Goal:** Use Copilot agent mode to scaffold a real project workspace in your language of choice. You'll use this project throughout the rest of the workshop.

**Time:** ~10 minutes

---

## Step 1 — Open Copilot Chat in Agent Mode

1. Open VS Code in this workshop folder (or a new empty folder where you want your project to live)
2. Open Copilot Chat: `Ctrl+Shift+I` / `Cmd+Ctrl+I`, or click the Copilot icon in the sidebar
3. In the chat input, click the mode selector and choose **Agent**

> **Why agent mode?** Agent mode can create multiple files, run terminal commands, and verify its own output — perfect for scaffolding an entire project from scratch.

---

## Step 2 — Run the Scaffold Prompt

Copy and paste the following prompt into the Copilot Chat input and press Enter:

```
I'm setting up a new project. Before you start, ask me the following questions one at a time and wait for my answers:

1. What programming language and framework (if any) should I use?
2. What should this project do? (e.g., REST API, CLI tool, web app, data pipeline, library)
3. Are there any specific libraries, patterns, or conventions I should follow?

Once I've answered all three questions, scaffold the full project workspace for me, including:

- A realistic folder structure appropriate for the project type
- A README.md with clear setup and run instructions
- All necessary config files (e.g., .gitignore, linter config, formatter config)
- A working entry point I can run immediately to verify the setup
- At least one example test to confirm the test runner is wired up correctly

After creating all the files, tell me the exact commands I need to run to install dependencies and verify everything works.
```

Answer Copilot's questions when it asks them, then let it build the project.

---

## Step 3 — Verify the Output

Run the commands Copilot gives you at the end to confirm the project starts and the test passes.

---

## Reflection Questions

Discuss with the group:

- Did Copilot ask clarifying questions before building, or did it make assumptions?
- How many files did it create? Was the folder structure what you expected?
- Did it run any terminal commands on its own (e.g., install dependencies)?
- Did the project actually run on the first try? If not, what needed fixing?
- Compare with someone using a different language — how different were the outputs?

---

## What's Next?

You now have a real project workspace to use for the rest of the workshop. Head to [01 — Agent Mode](../01-agent-mode/README.md).

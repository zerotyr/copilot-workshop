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

---

## Guided Path: Scaffold `snip`

> **Following the guided path?** Use the prompt below instead of the open-ended one above. It will scaffold a specific project — a command-line note manager called `snip` — that you'll extend in every subsequent exercise.

### What You're Building

`snip` is a minimal CLI tool for saving and retrieving short notes from the command line:

```
snip add "standup" "mention the auth refactor and the CI fix"
snip list
snip get "standup"
snip delete "standup"
```

Notes are stored as a JSON file (`notes.json`) in the current directory. No external services, no database — just plain files and standard library code.

### Step 1 — Pick Your Language

Decide which programming language and runtime you'll use. The tool works equally well in Python, Node.js, Go, Java, Ruby, Rust, C#, or any other language with file I/O and argument parsing support.

### Step 2 — Run the Scaffold Prompt

Copy and paste this prompt into Copilot Chat in **Agent** mode. Replace `[YOUR LANGUAGE]` with your choice.

```
I want to build a simple command-line note-taking tool called "snip" in [YOUR LANGUAGE].

It should support these subcommands:
- add <title> <content>  — Save a new note with the given title and content
- list                   — Print all saved notes (title + first 60 characters of content)
- get <title>            — Print the full content of a note by its exact title
- delete <title>         — Remove a note by its exact title

Storage: save all notes as a JSON array in a file called notes.json in the current directory.
Each note object should have "title" and "content" fields.

Scaffold the full project including:
- A realistic folder structure for a [YOUR LANGUAGE] CLI project
- A working entry point I can run immediately (e.g., `python snip.py add "hello" "world"`)
- A storage module that handles all reading and writing of notes.json
- A CLI module that parses the subcommand and delegates to the right logic
- At least 3 tests: one for add, one for list, one for delete
- A README.md with exact commands to install dependencies and run the tool

After creating all files, tell me the exact commands to install dependencies, run the tests,
and verify the tool works end-to-end.
```

### Step 3 — Verify the Scaffold

Run the commands Copilot gives you. Confirm:

1. The tests pass
2. You can add a note: `snip add "test" "hello world"`
3. You can list it: `snip list`
4. You can retrieve it: `snip get "test"`
5. You can delete it: `snip delete "test"`

---

## What's Next?

You now have a working `snip` project to use for the rest of the workshop. Head to [01 — Agent Mode](../01-agent-mode/README.md).

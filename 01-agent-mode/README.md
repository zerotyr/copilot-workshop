# 01 — Agent Mode

**Goal:** Understand what makes agent mode different from regular Copilot chat, and experience its autonomous multi-step execution firsthand.

**Time:** ~15 minutes

---

## What Is Agent Mode?

Standard Copilot chat answers questions and suggests code — but *you* apply the changes and run the commands.

**Agent mode is different.** It can:

- Read and write multiple files across your project simultaneously
- Run terminal commands and observe their output
- Detect errors (compile failures, test failures) and correct them automatically
- Iterate through a loop of read → write → run → verify until the task is done

Think of it less like a chatbot and more like a junior developer you can delegate a task to.

---

## How to Use Agent Mode

1. Open Copilot Chat (`Ctrl+Shift+I` / `Cmd+Ctrl+I`)
2. Click the mode selector in the chat input and choose **Agent**
3. Give it a task — be specific about the goal, not the steps

Agent mode will show you each action it's taking (opening files, running commands, editing code) in real time. You can stop it at any point.

---

## Sample Prompts to Try

Use your project from the Getting Started exercise. Try one or more of these:

**Task delegation:**
```
Add input validation to every function or endpoint in this project.
After each change, run the tests to confirm nothing is broken.
```

**Discovery + implementation:**
```
Find every TODO comment in the codebase and implement each one.
Run the tests when you're done to confirm everything still passes.
```

**Refactoring:**
```
Find all hardcoded string literals in the source code and extract them
into a single constants or configuration file. Update all references.
Do not change any behavior.
```

**Setup and verification:**
```
Set up this project from scratch. Install all dependencies, run the tests
to confirm they pass, then start the development server.
```

---

## Things to Watch

As agent mode runs, pay attention to:

- **Which files it opens** — does it explore before editing, or dive straight in?
- **Terminal output** — does it read the results of commands before deciding what to do next?
- **Self-correction** — if something fails, does it detect the error and adjust?
- **Scope** — does it stay focused on the task, or does it change things you didn't ask about?

---

## Chat vs. Agent Mode — Side-by-Side

Try this to see the difference clearly:

1. Switch to **Chat** mode
2. Paste one of the prompts above
3. Notice you get a plan or a code suggestion — but nothing happens automatically
4. Switch to **Agent** mode
5. Paste the same prompt
6. Watch it actually execute

---

## Reflection Questions

- How many files did agent mode touch for a single task?
- Did it run terminal commands? What did it do with the output?
- Did it have to make more than one pass to get the result right?
- Was there anything it did that surprised you — positively or negatively?
- When would you trust agent mode to run unsupervised vs. when would you want to review each step?

---

## What's Next?

[02 — GitHub Copilot CLI](../02-copilot-cli/README.md)

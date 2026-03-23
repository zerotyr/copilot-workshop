# 03 — Context Engineering

**Goal:** Understand what Copilot can "see" when you send a prompt, and learn how to give it the right context to get significantly better results.

**Time:** ~15 minutes

---

## What Is Context Engineering?

The quality of Copilot's output depends directly on what information it has access to when you ask. Two developers asking the exact same prompt can get very different results — because Copilot sees different context.

Context engineering is the practice of **deliberately controlling what Copilot sees** so it has everything it needs to give a useful answer.

---

## What Copilot Can See

By default, Copilot has access to:

- The **currently active file** (what you have open in the editor)
- **Open tabs** in your editor
- Any **`#` references** you include in your prompt
- Your **`.github/copilot-instructions.md`** file (if it exists)

It does *not* automatically read your whole codebase. You have to tell it what's relevant.

---

## Context Reference Syntax

Use these in Copilot Chat to point it at specific information:

| Reference | What it includes |
|---|---|
| `#file:path/to/file.ts` | The full contents of a specific file |
| `#folder:src/utils` | All files inside a folder |
| `@workspace` | Lets Copilot search across all files in the workspace |
| An open tab | Any file open in an editor tab is automatically included |

---

## Techniques to Try

### 1. Reference a Specific File

Instead of describing your data model from memory, point Copilot directly at it:

```
#file:src/models/user.ts Add a method that returns the user's full name.
```

```
Looking at #file:src/routes/auth.ts — what are all the possible error states this endpoint can return?
```

### 2. Cross-Reference Multiple Files

Ask Copilot to reason across multiple files at once:

```
Using #file:database/schema.sql and #file:src/models/product.ts,
check whether the model fields match the schema columns. List any mismatches.
```

```
Given #file:src/services/payment.ts and #file:src/tests/payment.test.ts,
what scenarios are currently untested?
```

### 3. Use `@workspace` for Discovery

When you don't know which file something is in:

```
@workspace Where is authentication handled in this project?
```

```
@workspace Are there any places where database queries are made directly in a controller instead of a service?
```

### 4. Use Inline Comments as Context

Before asking for a completion, write a comment that describes exactly what you want:

```python
# Parse the CSV file, skip the header row, and return a list of dicts
# where keys come from the header and values are stripped of whitespace
```

Then position your cursor below the comment and trigger an inline completion.

---

## Exercise: Context Makes the Difference

1. Pick a file in your project that has a dependency on another file (e.g., a service that uses a model)
2. Ask Copilot a question about it *without* any `#file` references — note the result
3. Ask the same question again, but add `#file:` references to the relevant files
4. Compare the two answers — what changed?

---

## Reflection Questions

- How did adding context references change the quality of the response?
- Were there cases where `@workspace` was more useful than a specific `#file` reference?
- What information would you always want Copilot to have for your specific project?
- How could you encode that persistent context so you don't have to add it every time? *(Hint: next topic)*

---

## Guided Path: Context Experiments with `snip`

> **Following the guided path?** These three experiments demonstrate context quality differences directly on your `snip` project.

### Experiment 1 — No context vs. file context

**Round 1 — without context:**
```
How should I add a --format flag to the list command that switches between plain text and JSON output?
```

Note the response. Is it generic? Does it reference the right files and functions?

**Round 2 — with file references** (adjust the file paths to your actual project structure):
```
Using #file:src/cli.py and #file:src/storage.py, how should I add a --format flag to
the list command that switches between plain text (default) and JSON output?
Which file should change? What's the minimal change needed?
```

Compare the two answers. The second should name specific functions and show exactly where to add the flag.

### Experiment 2 — Cross-file reasoning

```
Using #file:src/cli.py and #file:tests/test_snip.py, which subcommands currently
have test coverage and which ones are missing tests entirely?
```

This requires Copilot to correlate the implementation file with the test file — it can only do that if you explicitly give it both.

### Experiment 3 — Discovery with `@workspace`

When you don't know exactly where something lives:
```
@workspace Where is the JSON file path defined in this project?
Is it hardcoded, or is there a way to configure it?
```

Then follow up without any `@workspace`:
```
What would need to change to make the storage path configurable via an environment variable?
```

Note how the follow-up can reference what was just discovered — Copilot carries context through the conversation.

---

## What's Next?

[04 — Prompt Engineering](../04-prompt-engineering/README.md)

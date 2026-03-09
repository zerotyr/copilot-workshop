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

## What's Next?

[04 — Prompt Engineering](../04-prompt-engineering/README.md)

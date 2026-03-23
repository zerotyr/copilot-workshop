# 06 — Prompt Files

**Goal:** Create reusable, version-controlled prompt templates that you and your team can invoke directly from Copilot Chat.

**Time:** ~15 minutes

---

## What Are Prompt Files?

Prompt files are markdown files stored in `.github/prompts/` that Copilot can invoke directly from chat using the `#` reference syntax. They let you:

- **Standardize** repeated tasks so everyone on the team runs them the same way
- **Share** carefully crafted prompts as first-class project artifacts
- **Document intent** — the prompt file itself explains what the task is and how to do it

Prompt files are checked into your repository alongside your code. They're a team asset, not a personal shortcut.

---

## File Format

Prompt files use a YAML frontmatter block followed by a markdown prompt body.

```
.github/prompts/your-prompt-name.prompt.md
```
> Note: no frontmatter (the stuff between the `---`) are required for prompt files

```markdown
---
name: prompt-me
description: A short description shown in the Copilot UI
---

Your prompt text goes here. Write it exactly as you'd write it
in the Copilot Chat input.

You can reference files using #file: syntax, use variables like
[PLACEHOLDER], or describe multi-step tasks.
```

For more frontmatter options, see [prompt files in VS code](https://code.visualstudio.com/docs/copilot/customization/prompt-files).

---

## Example Prompt Files

### Add a new CRUD resource

```markdown
---
name: crud
description: Add a new resource with full CRUD operations
---

Add a new [RESOURCE_NAME] resource to this project with full CRUD operations.

Follow the existing patterns in the codebase exactly — the same file structure,
naming conventions, and error handling patterns already in use.

Include:
- Model or schema definition
- All CRUD operations (list, get by ID, create, update, delete)
- Input validation
- At least one test per operation covering the happy path

After creating the files, run the tests to confirm they all pass.
```

---

### Code review checklist

```markdown
---
name: review
description: Review staged changes for common issues
---

Review the changes in the currently open file. Check for:

1. Security issues: injection vulnerabilities, exposed secrets, improper auth checks
2. Missing input validation on any data coming from outside the system
3. Error cases that aren't handled (missing null checks, uncaught exceptions)
4. Any violation of the rules in .github/copilot-instructions.md
5. Missing or inadequate test coverage for the changed logic

Format your findings as a list. For each issue, include:
- [SEVERITY: HIGH / MED / LOW]
- What the problem is
- A specific suggestion to fix it
```

---

### Generate documentation

```markdown
---
name: doc
description: Generate documentation for a module or file
---

Generate comprehensive documentation for #file:[TARGET_FILE].

Include:
- An overview section explaining what this module does and when to use it
- A description of every exported function, class, or type including:
  - What it does
  - Each parameter (name, type, what it's for)
  - Return value
  - Any exceptions or error states it can produce
- At least one usage example per public function

Write the documentation as inline docstrings/JSDoc in the source file,
and also produce a standalone [TARGET_FILE].md next to the source file.
```

---

## Exercise

1. Think of a task you do repeatedly in your project (e.g., adding a new route, writing a migration, generating a test suite for a file)
2. Create `.github/prompts/` in your project if it doesn't exist
3. Write a prompt file for that task — give it a clear name and a useful description
4. In Copilot Chat, type `#` and find your prompt file in the list
5. Run it on a real task in your project

---

## Invoking a Prompt File

In Copilot Chat, type `#` to open the reference picker. Your prompt files will appear in the list. Select one to insert it into your chat input — you can then fill in any `[PLACEHOLDER]` values before sending.

---

## Reflection Questions

- What tasks in your daily workflow are good candidates for prompt files?
- How is a prompt file different from a code snippet or a script?
- Who on your team should write and maintain prompt files?
- How would you handle a prompt file that gets out of date as the codebase evolves?
- What's the relationship between prompt files and custom instructions?

---

## Guided Path: A Reusable Subcommand Template for `snip`

> **Following the guided path?** Follow these steps to create a prompt file that makes adding any new subcommand to `snip` a one-line task.

### Step 1 — Create the prompt file

Create the file `.github/prompts/add-subcommand.prompt.md` in your `snip` project:

```markdown
---
name: add-subcommand
description: Add a new subcommand to the snip CLI
---

Add a new subcommand called `[SUBCOMMAND_NAME]` to the snip CLI.

What it should do: [DESCRIPTION]

Follow the existing subcommand patterns exactly:
- Parse arguments in the CLI module — no business logic in the parser
- Implement the logic using the storage module — no direct file access elsewhere
- Print a human-readable confirmation on success (e.g., "Done: [SUBCOMMAND_NAME]")
- Print errors to stderr and exit with code 1 on failure
- Add at least one happy path test and one error path test
- Tests must use a temporary file or mocked storage — never the real notes.json

After creating all files, run the tests and confirm they pass.
```

### Step 2 — Use the prompt file

1. In Copilot Chat (agent mode), type `#` and select `add-subcommand` from the picker
2. Fill in the two placeholders:
   - `[SUBCOMMAND_NAME]` → `count`
   - `[DESCRIPTION]` → `Print the total number of saved notes. Output format: "X notes saved." Exit with code 0 even if there are no notes.`
3. Send the completed prompt

### Step 3 — Use it again immediately

Without writing anything from scratch, use the same prompt file again to add a `copy` subcommand:
- `[SUBCOMMAND_NAME]` → `copy`
- `[DESCRIPTION]` → `Print the content of the note with the given title to stdout, prefixed with "---". This makes it easy to pipe into other commands. Exit with code 1 if the note does not exist.`

Notice how the same template produced two different, correctly structured subcommands. The prompt file captured the pattern once and applied it twice.

---

## What's Next?

[07 — Custom Agents](../07-custom-agents/README.md)

# 05 — Custom Instructions

**Goal:** Learn how to define persistent, repo-level rules that Copilot automatically applies to every interaction in your project — without having to repeat yourself in every prompt.

**Time:** ~15 minutes

---

## What Are Custom Instructions?

The file `.github/copilot-instructions.md` in your repository is automatically read by GitHub Copilot on every interaction. Anything you write there becomes part of Copilot's context for that repo — for you *and* for everyone on your team.

Use it to encode:

- Coding conventions and style rules
- Architectural patterns your project follows
- Things Copilot should always or never do in this codebase
- Project-specific terminology or concepts

---

## Creating the File

In your project, create the file at:

```
.github/copilot-instructions.md
```

Write your rules in plain English — no special syntax required. Full markdown is supported.

---

## Example Instructions

The rules below are language-agnostic starting points. Adapt them to fit your project's conventions.

```markdown
## Code Style

- Write a docstring or JSDoc comment for every public function and class.
- Use named constants instead of magic numbers or magic strings.
- Prefer composition over inheritance.

## Architecture

- All database access must go through service or repository classes.
  Never query the database directly from a controller or route handler.
- Keep business logic out of API handlers — handlers should only
  validate input, call a service, and format a response.

## Error Handling

- All error messages must be human-readable and include the name of
  the affected resource (e.g., "User not found: id=42").
- Never swallow exceptions silently — either handle them explicitly
  or let them propagate to a top-level error handler.

## Testing

- Every new function should have at least one test covering the
  happy path and one covering an error or edge case.
- Do not mock internal modules — only mock external dependencies
  (databases, HTTP clients, file system).
```

---

## Exercise

### Part A — Write Your Instructions (~5 min)

1. Create `.github/copilot-instructions.md` in your project
2. Write 3–5 rules that reflect real conventions in your codebase (or conventions you *wish* it followed)
3. Save the file

### Part B — Observe the Effect (~10 min)

Run this prompt (or adapt it to something relevant to your project):

```
Add a new feature to this project. Create a new [resource or module]
with the appropriate handler, service, and tests. Follow the existing
patterns in the codebase.
```

Watch whether Copilot follows the rules you defined — docstrings, architecture patterns, error message format, etc.

**To make the comparison clear:** run the same prompt in a project *without* a `copilot-instructions.md` and compare the outputs.

---

## Facilitator Tip

Show the instructions file appearing as a reference in the Copilot Chat context indicator ("Used 1 file"). This makes it visible that Copilot is actively reading it — it's not magic, it's just context.

---

## Reflection Questions

- Did Copilot apply your rules without being explicitly asked?
- Were any rules ignored or only partially followed?
- What rules would be most valuable for your team to standardize?
- Who should own this file in a real project? How would you maintain it?
- How is this different from adding the same rules to every prompt manually?

---

## What's Next?

[06 — Prompt Files](../06-prompt-files/README.md)

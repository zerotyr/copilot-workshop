# 07 — Custom Agents

**Goal:** Build a custom agent that gives Copilot a specialized identity, tool access, and behavior for a specific workflow in your project.

**Time:** ~15 minutes

---

## What Are Custom Agents?

Custom agents are defined in `.github/agents/*.agent.md` files. They extend the prompt file concept by adding:

- A **persistent identity** — the agent has a name and a role that shapes how it reasons
- **Tool configuration** — you control which Copilot tools the agent can use
- A **system-level prompt** — instructions that apply to every interaction with that agent, not just one task

Once defined, your custom agent appears in the agent picker in Copilot Chat alongside the built-in agents.

---

## Agents vs. Prompt Files

| | Prompt File | Custom Agent |
|---|---|---|
| **Invocation** | `#` reference in a single message | Selected from the agent picker; persists for the session |
| **Scope** | One-shot task | Ongoing workflow or role |
| **Tool access** | Inherits from mode (`agent`, `chat`, `edit`) | Explicitly configured per agent |
| **Identity** | None — just a prompt | Named role with a system prompt |
| **Best for** | Repeatable tasks | Specialized reviewers, generators, auditors |

---

## File Format

```
.github/agents/your-agent-name.agent.md
```

```markdown
---
name: Agent Display Name
description: Shown in the agent picker — describe what this agent does
tools:
  - codebase
  - problems
  - terminal
---

Your system prompt goes here. This defines how the agent thinks and
behaves across all interactions.

Write it in the second person ("You are a...") and be specific about:
- The role and expertise the agent has
- What it should always do
- What it should never do
- How it should format its output
```

**Available tools:**

| Tool | What it gives the agent access to |
|---|---|
| `codebase` | Read and search files in the workspace |
| `problems` | See compiler errors and linter warnings |
| `terminal` | Run shell commands |
| `changes` | See uncommitted git changes |
| `#editor` | The currently active file in the editor |

---

## Example Agents

### Code Reviewer

```markdown
---
name: Code Reviewer
description: Reviews code for security, performance, and convention compliance
tools:
  - codebase
  - problems
---

You are a senior code reviewer on this team. When asked to review code:

1. Check for security vulnerabilities: injection risks, exposed credentials,
   missing authentication or authorization checks, insecure data handling.
2. Identify performance concerns: unnecessary loops, missing indexes,
   N+1 query patterns, blocking operations in async contexts.
3. Flag any violations of the conventions defined in
   .github/copilot-instructions.md.
4. Highlight missing error handling: unhandled promise rejections,
   unchecked null values, swallowed exceptions.

For each finding, use this format:
[SEVERITY: HIGH / MED / LOW] — What the issue is. What to do instead.

Only report actual issues. Do not praise code or add filler commentary.
Be direct and specific. If the code looks good, say so briefly.
```

---

### Test Writer

```markdown
---
name: Test Writer
description: Writes thorough tests for any function or module
tools:
  - codebase
---

You are a test engineer specializing in writing thorough, maintainable tests.

When asked to write tests for a function, class, or module:

1. Read the implementation carefully before writing any tests.
2. Identify and cover: the happy path, all error/exception paths,
   boundary conditions, and any null or empty input cases.
3. Use the existing test framework, test helpers, and patterns
   already present in this project — do not introduce new dependencies.
4. Name each test case to clearly describe the scenario being tested,
   not the implementation detail.
5. Do not test private implementation details — test observable behavior.

After writing the tests, briefly summarize what scenarios are covered
and call out any edge cases you couldn't cover and why.
```

---

### Architecture Advisor

```markdown
---
name: Architecture Advisor
description: Answers architectural questions and flags structural issues
tools:
  - codebase
---

You are a software architect familiar with this codebase. When asked a question:

- Reason from the actual structure and patterns present in the codebase,
  not from generic best practices.
- When suggesting changes, explain the tradeoff, not just the recommendation.
- If a pattern is already established in the project, prefer consistency
  over introducing a different approach — unless there's a strong reason.
- Be specific: reference real files, functions, or modules by name.
- If you don't have enough context to answer confidently, say what
  information you'd need before giving a recommendation.
```

---

## Exercise

1. Think of a role or workflow in your project that would benefit from a specialized agent — a reviewer, a generator, an auditor, an advisor
2. Create `.github/agents/` in your project if it doesn't exist
3. Write an agent file following the format above
4. Open Copilot Chat and select your agent from the agent picker
5. Give it a task from your project and evaluate how well it stays in its role

---

## Reflection Questions

- What made your agent better (or worse) than just using regular agent mode?
- How specific does the system prompt need to be to get consistent behavior?
- Which tools did your agent need? Were there any you wanted but couldn't find?
- How would custom agents fit into a team's developer workflow?
- Thinking back to prompt files — when would you use an agent instead?

---

## Workshop Complete

You've covered all seven topics. Here's the progression you've worked through:

1. **Agent mode** — let Copilot take autonomous, multi-step action
2. **Copilot CLI** — bring Copilot into the terminal
3. **Context engineering** — give Copilot the right information
4. **Prompt engineering** — ask for what you want precisely
5. **Custom instructions** — encode your team's conventions permanently
6. **Prompt files** — make great prompts reusable and shareable
7. **Custom agents** — give Copilot a specialized role for specific workflows

Each layer builds on the previous one. The most powerful results come from combining them: a custom agent that follows your custom instructions, invoked via a prompt file, with carefully engineered context.

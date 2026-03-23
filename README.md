# GitHub Copilot Workshop

A hands-on, facilitator-led workshop exploring GitHub Copilot's most powerful features. All exercises are **language-agnostic** — bring whatever project and tech stack you already work with.

---

## Prerequisites

Before the workshop, make sure you have the following installed and working:

| Requirement | Notes |
|---|---|
| VS Code | Latest stable release |
| GitHub Copilot extension | Sign in with your GitHub account |
| GitHub Copilot CLI | `winget install GitHub.Copilot` or `brew install copilot-cli` or `curl -fsSL https://gh.io/copilot-install \| bash` — [docs](https://docs.github.com/copilot/concepts/agents/about-copilot-cli) |
| GitHub Copilot CLI (Windows only) | Powershell v6 or higher |
| Your preferred language runtime | e.g., Node.js, Python, Java, Go, etc. |

Verify Copilot CLI is working:

```sh
copilot --version
```

---

## How to Use This Workshop

### Option A — Bring Your Own Project
1. Start with **Getting Started** — use the scaffold prompt to create a project workspace in your language of choice. You'll use this project throughout all exercises.
2. Work through the numbered topics in order, or jump to any topic that interests you — each section is self-contained.
3. Every topic has **sample prompts to try** and **reflection questions** to discuss with the group.

### Option B — Follow the Guided Path
Every exercise includes a **Guided Path** section with explicit, step-by-step instructions for building a simple command-line tool called `snip`. If you'd rather follow a concrete path than bring your own project, look for the **Guided Path** section in each exercise.

> **What is `snip`?** A minimal command-line note manager. You'll build it from scratch in your language of choice and extend it across every exercise — adding subcommands, validation, tests, and tooling one step at a time.

> **Tip for facilitators:** Pause after each exercise to collect observations from the group. The best learning moments come from comparing what different participants got from the same prompt.

---

## Topics

| # | Topic | Key Concept | Est. Time |
|---|---|---|---|
| 0 | [Getting Started](./getting-started/README.md) | Scaffold your project workspace with agent mode | 10 min |
| 1 | [Agent Mode](./01-agent-mode/README.md) | Autonomous multi-step task execution | 15 min |
| 2 | [GitHub Copilot CLI](./02-copilot-cli/README.md) | Shell command suggestions and explanations | 10 min |
| 3 | [Context Engineering](./03-context-engineering/README.md) | Giving Copilot the right information | 15 min |
| 4 | [Prompt Engineering](./04-prompt-engineering/README.md) | Writing prompts that produce better results | 15 min |
| 5 | [Custom Instructions](./05-custom-instructions/README.md) | Persistent repo-level rules for every interaction | 15 min |
| 6 | [Prompt Files](./06-prompt-files/README.md) | Reusable, shareable prompt templates | 15 min |
| 7 | [Custom Agents](./07-custom-agents/README.md) | Specialized agents for specific workflows | 15 min |

**Total estimated time:** ~1.5–2 hours

---

## A Note on Language

Every exercise is designed to work with **any programming language or framework**. Sample prompts use generic language — adapt them to your project as you go. The goal is to learn how to work with Copilot, not to learn a specific technology.

---

## Troubleshooting

Having issues? See [troubleshooting Copilot](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/troubleshoot-copilot/troubleshoot-common-issues).

---

CC-BY-NC

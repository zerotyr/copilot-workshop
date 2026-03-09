# 04 — Prompt Engineering

**Goal:** Learn the principles of writing prompts that produce specific, correct, and predictable results — and practice refining prompts through iteration.

**Time:** ~15 minutes

---

## What Is Prompt Engineering?

Prompt engineering is the practice of crafting your request to Copilot so that it has enough information to do exactly what you want. It's not about magic words — it's about **being precise about the goal, constraints, and expected output**.

A well-engineered prompt produces a result you can use immediately. A vague prompt produces a result you have to fix, re-prompt, or throw away.

---

## Core Principles

### 1. Be specific about the goal
State what you want done, not just that something should change.

### 2. State constraints explicitly
What should it *not* do? What patterns should it follow? What must stay the same?

### 3. Reference the relevant context
Point to the files, functions, or patterns it should use (see Topic 03).

### 4. Describe the output format
If you want a specific structure, say so. Code? A list? A table? A function with a specific signature?

### 5. Give an example when the pattern is non-obvious
If your project uses a specific convention, show it one example to follow.

---

## Before & After: Prompt Pairs

Study these examples, then think about how they apply to your own project.

---

### Bug Fix

❌ **Vague:**
```
Fix this function.
```

✅ **Specific:**
```
This function throws a KeyError when the input dictionary is missing
the 'user_id' key. Add a guard clause at the top that raises a
ValueError with the message "Missing required field: user_id" instead
of letting it crash with a KeyError.
```

---

### Adding Tests

❌ **Vague:**
```
Add tests for this.
```

✅ **Specific:**
```
Write unit tests for the calculate_discount function in #file:src/pricing.ts.
Cover these cases: zero input, negative input, a value above the maximum
allowed discount (100), and the normal happy path.
Use the existing test framework and helper patterns already in the test files.
```

---

### Refactoring

❌ **Vague:**
```
Refactor this file.
```

✅ **Specific:**
```
Extract the database connection setup from #file:src/app.ts into a
separate src/db.ts module. Export a single connection function.
Update all files that currently import or reference the connection
directly. Do not change any business logic or query behavior.
```

---

### Adding a Feature

❌ **Vague:**
```
Add pagination.
```

✅ **Specific:**
```
Add pagination to the list endpoint in #file:src/routes/products.ts.
Accept 'page' (default: 1) and 'limit' (default: 20, max: 100) as
query parameters. Return the results along with a 'meta' object
containing 'total', 'page', 'limit', and 'totalPages'.
Follow the same response structure used by the existing list endpoints.
```

---

## Advanced Techniques

Once you're comfortable with the basics, these techniques produce consistently better results on complex tasks.

---

### Few-Shot Prompting

Show Copilot one or more examples of the pattern you want it to follow before asking it to do the real task. This is especially effective when your project uses unconventional conventions that can't be inferred from description alone.

**Without examples:**
```
Add a validation function for the Order model.
```

**With examples (few-shot):**
```
Here's how we write validation functions in this project:

// Example 1
function validateUser(data: unknown): Result<User, ValidationError[]> {
  const errors: ValidationError[] = [];
  if (!data.email) errors.push({ field: 'email', message: 'required' });
  if (!isValidEmail(data.email)) errors.push({ field: 'email', message: 'invalid format' });
  return errors.length ? err(errors) : ok(data as User);
}

// Example 2
function validateAddress(data: unknown): Result<Address, ValidationError[]> {
  const errors: ValidationError[] = [];
  if (!data.street) errors.push({ field: 'street', message: 'required' });
  if (!data.postcode) errors.push({ field: 'postcode', message: 'required' });
  return errors.length ? err(errors) : ok(data as Address);
}

Now write a validateOrder function that checks: customerId (required),
items (required, non-empty array), and totalAmount (required, must be > 0).
```

**When to use it:** Custom return types, unusual error handling patterns, project-specific abstractions, or any time "follow the existing pattern" isn't enough because the pattern is hard to discover automatically.

---

### Step-by-Step Prompting

Break a complex task into an explicit sequence of steps inside the prompt itself. This forces Copilot to plan before acting and produces more coherent results on multi-part tasks.

**Without steps:**
```
Migrate the user authentication system from sessions to JWT.
```

**With explicit steps:**
```
Migrate the user authentication system from sessions to JWT.
Work through this in the following order:

1. Read the current session-based auth implementation in #file:src/auth/session.ts
   and list every function that will need to change.
2. Add the jsonwebtoken dependency to package.json.
3. Create src/auth/jwt.ts with generateToken, verifyToken, and refreshToken functions.
4. Update the login endpoint to issue a JWT instead of setting a session cookie.
5. Replace the session middleware in src/middleware/auth.ts with JWT verification.
6. Update the logout endpoint to handle stateless token invalidation.
7. Run the tests. Fix any failures before moving on.

Do not skip steps or combine them. Show me what you find in step 1 before proceeding.
```

**When to use it:** Migrations, multi-file refactors, any task where the order of changes matters, or when previous attempts produced incomplete results.

---

### RAG-Style Prompting (Retrieval-Augmented)

RAG is typically a backend architecture, but the underlying principle applies directly to prompting: **explicitly retrieve and inject relevant context** before asking your question, rather than hoping Copilot finds it on its own.

In practice this means pulling in the specific files, schemas, or reference material that Copilot needs to reason accurately — instead of asking a broad question and getting a hallucinated answer.

**Without retrieved context:**
```
Why is the checkout endpoint returning a 500 error?
```

**With explicitly retrieved context:**
```
Here is the relevant context for this debugging task:

- The failing endpoint: #file:src/routes/checkout.ts
- The service it calls: #file:src/services/order.ts
- The database schema for orders: #file:database/migrations/003_orders.sql
- The most recent error from the logs:
  TypeError: Cannot read properties of undefined (reading 'items')
  at OrderService.createOrder (src/services/order.ts:47)

Given this context, explain what is causing the error and fix it.
```

**When to use it:** Debugging across multiple files, any time Copilot has previously given wrong answers because it lacked context, or when working in a large codebase where `@workspace` search isn't precise enough.

---

### Step-Back Prompting

Before diving into implementation, ask Copilot to "step back" and reason about the higher-level problem first — principles, tradeoffs, or root causes. Then use that reasoning to inform the implementation prompt.

This is a two-turn technique: the first prompt produces understanding, the second produces code.

**Turn 1 — Step back:**
```
Before we write any code: what are the key tradeoffs between storing user
sessions in a database vs. using stateless JWTs for a web application?
Consider: scalability, security, revocation, and implementation complexity.
```

**Turn 2 — Apply the reasoning:**
```
Given the tradeoffs you just described, and the fact that our app needs to
support immediate token revocation for compliance reasons, implement a
hybrid approach: short-lived JWTs (15 min) with a refresh token stored in
the database. Use #file:src/auth/session.ts as the starting point.
```

**Another example — root cause before fix:**

**Turn 1:**
```
Looking at #file:src/services/cache.ts — without making any changes,
explain what assumptions this caching layer makes about data consistency,
and where those assumptions could break down under concurrent writes.
```

**Turn 2:**
```
Based on the race condition you identified in the previous step, add
appropriate locking to prevent it. Use the existing Redis client already
configured in this project.
```

**When to use it:** Architectural decisions, debugging subtle or intermittent bugs, security-sensitive changes, or any time you want Copilot's reasoning visible before it acts.

---

## Anti-Patterns to Avoid

| Anti-pattern | Why it's a problem |
|---|---|
| Vague verbs: "improve", "fix", "clean up" | No clear success condition — Copilot will guess |
| No context: asking about code that isn't open or referenced | Copilot invents details |
| Too many things at once | Results become inconsistent or incomplete |
| No constraints: "make it better" | "Better" is subjective — it might change things you didn't want changed |
| Asking for a result without specifying the interface | You get code that works but doesn't fit your architecture |

---

## Exercise: Write → Run → Evaluate → Refine

1. Pick a concrete task in your project (e.g., add a new function, fix a bug, write a test)
2. Write a first-draft prompt and run it in Copilot Chat or agent mode
3. Evaluate the result: What was right? What was wrong or missing?
4. Rewrite the prompt applying the principles above
5. Run it again and compare

Share your before/after prompts with the group — the discussion is often more valuable than the code.

---

## Reflection Questions

- What was the most common reason your first-draft prompt produced a suboptimal result?
- How much extra time did you spend writing a detailed prompt vs. fixing a vague result?
- Is there a type of task where a vague prompt is actually fine?
- How does good prompt engineering relate to good communication with a human developer?

---

## What's Next?

[05 — Custom Instructions](../05-custom-instructions/README.md)

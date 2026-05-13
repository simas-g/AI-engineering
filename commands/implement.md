---
name: implement
description: Implement a GitHub issue end-to-end with minimal back-and-forth. Pass an issue number as argument. Reads the issue, plans briefly, confirms with user once, then implements and runs tests autonomously.
---

# Implement

Implement a GitHub issue autonomously. One confirmation checkpoint, then go.

## Usage

```
/implement 42
```

## Process

### 1. Read the issue

Fetch the full issue body and comments:

```
gh issue view <number> --comments
```

Extract:
- **What to build** — the end-to-end behavior description
- **Acceptance criteria** — the checkbox list; these become your test targets
- **Blocked by** — if blockers exist and aren't closed, stop and tell the user

### 2. Explore the codebase

Understand the current state before touching anything:

- Find the modules most relevant to this issue
- Read existing tests in the same area to understand conventions (test runner, assertion style, file layout)
- Check `CONTEXT.md` and `docs/adr/` if they exist — use the project's domain vocabulary throughout
- Identify the public interfaces you'll add or modify

### 3. Present a one-shot plan (the only checkpoint)

Show the user a brief plan in this format — keep it tight, no padding:

```
**Issue #<n>: <title>**

**What I'll build:**
<one paragraph, end-to-end behavior>

**Files I'll touch:**
- `path/to/file.ts` — <why>
- `path/to/test.ts` — <why>

**Public interface changes:**
<new or modified function/type signatures only — no implementation details>

**Test approach:**
<what behaviors I'll test and at what seam>

Good to go, or anything to redirect?
```

Wait for the user's response. If they say go (or anything affirmative), proceed. If they redirect, update the plan accordingly and confirm once more.

### 4. Implement

Work through the acceptance criteria top to bottom. For each criterion:

1. Write a test that will fail until the criterion is met
2. Implement just enough to make it pass
3. Move to the next criterion

Rules:
- Use public interfaces only in tests — no testing internal details
- Mock only at system boundaries (external APIs, email, payments, time) — never mock your own modules
- Minimum code to satisfy each criterion — do not add features beyond what the issue asks for
- Use the project's existing patterns: same test runner, same assertion style, same file structure

### 5. Run tests

Run the full test suite (or the nearest scoped suite if the full run takes too long). Fix any failures before reporting done.

Infer the test command from the project:
- `package.json` scripts → look for `test`, `test:unit`, `vitest`, `jest`
- `Makefile` → look for `make test`
- `pyproject.toml` / `pytest.ini` → `pytest`
- Otherwise ask the user

### 6. Report done

Post a short summary:

```
**Done — #<n>**

Criteria met:
- [x] criterion 1
- [x] criterion 2

Tests: <N> passed, 0 failed

Files changed: <list>
```

If any acceptance criterion could not be met, say so explicitly and why — do not mark it complete.

## Constraints

- Do not close or comment on the issue unless the user asks
- Do not push or open a PR unless the user asks
- Do not refactor code outside the scope of the issue
- If the issue is marked HITL (needs human judgment), stop after the plan and tell the user why it can't be implemented autonomously

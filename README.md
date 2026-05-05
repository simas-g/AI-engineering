# AI Engineering Skills

A collection of Claude Code slash commands for real engineering work — not vibe coding.

Developing real applications is hard. These skills are designed to be small, easy to adapt, and composable. They work with any model and are based on solid engineering fundamentals. Hack around with them. Make them your own.

## Install

Copy the skills to your Claude Code global commands folder:

```bash
cp commands/*.md ~/.claude/commands/
```

Or symlink for automatic sync when you pull updates:

```bash
ln -s $(pwd)/commands ~/.claude/commands
```

## Skills

- **[/diagnose](./commands/diagnose.md)** — Disciplined diagnosis loop for hard bugs and performance regressions: reproduce → hypothesise → instrument → fix → regression-test.
- **[/grill-me](./commands/grill-me.md)** — Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree.
- **[/improve-codebase-architecture](./commands/improve-codebase-architecture.md)** — Find deepening opportunities in a codebase, informed by the domain language in `CONTEXT.md` and the decisions in `docs/adr/`.
- **[/setup-matt-pocock-skills](./commands/setup-matt-pocock-skills.md)** — Per-repo setup: configure the issue tracker, triage label vocabulary, and domain doc layout for the other skills.
- **[/tdd](./commands/tdd.md)** — Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **[/to-issues](./commands/to-issues.md)** — Break any plan, spec, or PRD into independently-grabbable issues using tracer-bullet vertical slices.
- **[/to-prd](./commands/to-prd.md)** — Turn the current conversation context into a PRD and publish it to the project issue tracker.
- **[/triage](./commands/triage.md)** — Triage issues through a state machine of triage roles (needs-triage → ready-for-agent etc.).
- **[/zoom-out](./commands/zoom-out.md)** — Tell the agent to zoom out and map all relevant modules and callers for an unfamiliar section of code.

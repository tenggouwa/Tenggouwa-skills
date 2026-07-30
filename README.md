# Tenggouwa Skills

Reusable skills for Codex and ChatGPT.

## Install in Codex

Run this once to add the marketplace and install the plugin:

```bash
codex plugin marketplace add tenggouwa/Tenggouwa-skills && \\
  codex plugin add persistent-execution@tenggouwa-skills
```

For work that must not stop halfway, start an active Codex goal in a new task:

```text
/goal Use $persistent-execution to <state the outcome>. Do not finish until <state the verification evidence> passes.
```

For example:

```text
/goal Use $persistent-execution to finish the knowledge-graph remediation. Do not finish until the migration, tests, and CI are complete and the changed workflow has been verified.
```

`$persistent-execution` supplies the execution protocol; `/goal` is what keeps
the task active across multiple work cycles. A normal chat turn can still end
after a progress update, so it is not sufficient for a task that must continue
without a follow-up from you.

To update later:

```bash
codex plugin marketplace upgrade tenggouwa-skills && \\
  codex plugin add persistent-execution@tenggouwa-skills
```

## Included plugin

- [`persistent-execution`](./plugins/persistent-execution): Drive multi-step tasks through investigation, implementation, verification, and safe handoff.

## Local use

For direct development without the plugin installer, copy a skill directory into a Codex skill discovery location, such as:

- `<repo>/.agents/skills/` for repository-scoped workflows
- `~/.agents/skills/` for personal workflows

Each skill is self-contained and begins with a `SKILL.md` file. The plugin marketplace is defined in [`.agents/plugins/marketplace.json`](./.agents/plugins/marketplace.json).

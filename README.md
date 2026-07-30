# Tenggouwa Skills

Reusable skills for Codex and ChatGPT.

## Install in Codex

Run this once to add the marketplace and install the plugin:

```bash
codex plugin marketplace add tenggouwa/Tenggouwa-skills && \\
  codex plugin add persistent-execution@tenggouwa-skills
```

Start a new Codex task after installation, then invoke the skill as
`$persistent-execution` or use a request that matches its description.

To update later:

```bash
codex plugin marketplace upgrade tenggouwa-skills
```

## Included plugin

- [`persistent-execution`](./plugins/persistent-execution): Drive multi-step tasks through investigation, implementation, verification, and safe handoff.

## Local use

For direct development without the plugin installer, copy a skill directory into a Codex skill discovery location, such as:

- `<repo>/.agents/skills/` for repository-scoped workflows
- `~/.agents/skills/` for personal workflows

Each skill is self-contained and begins with a `SKILL.md` file. The plugin marketplace is defined in [`.agents/plugins/marketplace.json`](./.agents/plugins/marketplace.json).

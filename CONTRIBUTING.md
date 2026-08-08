# Contributing to AI-CAD Labs

These instructions apply across the **ai-cad-labs** repos;
the flagship, [`ai-cad`](https://github.com/ai-cad-labs/ai-cad),
is where almost all development happens.
You do not need to be a CAD veteran
or a machine-learning engineer to have a big impact:
documentation, DFM/DFA rule improvements, gallery runs,
and issue reports all move the project forward.

## Before you change anything

1. Read [`AGENTS.md`](https://github.com/ai-cad-labs/ai-cad/blob/main/AGENTS.md),
   the canonical map of the flagship repo for humans and coding agents alike.
   It also routes development-mode readers to the README's design principles;
   changes are expected to stay aligned with them.
2. The one convention that matters most:
   **edit canonical content in `.shared/` only**
   (`.claude/` and `.opencode/` are symlinks into it).
3. Run both test suites before opening a pull request:

   ```bash
   uv run --frozen pytest -q                  # tool layer
   cd frontend && npm ci && npx vitest run    # frontend
   ```

## Reporting a bug

Open an issue answering three questions:

1. **Your environment**: OS, Python version, and harness (Claude Code version if known).
2. **What you asked for**: the prompt, or the run's `goals.md`.
3. **What happened**: attach evidence from the run's project directory,
   ideally the tail of `design_log.md`, `open_issues.md`,
   and `run_reflection.md` if the run wrote one.

The project directory is the reproduction case:
it usually contains everything a maintainer needs.

## Suggesting a feature or a rule

Open an issue describing the change and why it matters.
DFM/DFA rule proposals are a first-class contribution surface:
the rulebooks in [`rules/`](https://github.com/ai-cad-labs/ai-cad/tree/main/rules)
have a documented proposal schema
(see the [`dfm-rules`](https://github.com/ai-cad-labs/ai-cad/tree/main/.shared/skills/dfm-rules) skill),
and rules can be proposed, promoted, or retired over time.

## Where to ask

Channels and self-serve help live in
[SUPPORT.md](https://github.com/ai-cad-labs/.github/blob/main/SUPPORT.md).

## Licensing

Every public **ai-cad-labs** repo ships under the Apache License 2.0,
each with its own LICENSE and NOTICE;
by contributing, you agree your contributions are licensed the same way.

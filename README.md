# python-domain-modeling

A Python domain-modeling plugin for coding agents. It covers valid domain states
and side-effect boundaries: encode invariants with types and explicit transitions,
then keep domain decisions predictable when code reads time, randomness, external
data, or mutable state.

This repository does not duplicate general Python tooling, testing,
documentation, planning, delegation, debugging, or code-review practices.
Use established skills such as Superpowers and Ponytail for those concerns.

## Install

Claude Code:
```bash
claude plugin marketplace add constatza/python-domain-modeling
claude plugin install python-domain-modeling@python-domain-modeling
```

Codex CLI:
```bash
codex plugin marketplace add constatza/python-domain-modeling
codex plugin add python-domain-modeling@python-domain-modeling
```

## Maintaining

`plugins/python-domain-modeling/plugin.json` is the hand-edited source of truth for
the plugin's version; `.claude-plugin/plugin.json` and `.codex-plugin/
plugin.json` are the per-host manifests and should be kept in sync with it by
hand (no build step — this repo has no code, just docs and skill files).

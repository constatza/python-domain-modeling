# python-domain-modeling

A deliberately narrow, Python-specific plugin for type-driven domain modeling.
It helps coding agents encode invariants with unions, state-specific frozen
dataclasses, semantic types, validated value objects, explicit transitions,
exhaustive matches, and boundary-to-domain conversion.

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

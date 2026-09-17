<div align="center">

# Agentic Kaggle Skill — Astra Slim

A lean Kaggle execution skill for capable coding agents such as GPT-6 Astra.

</div>

This fork keeps the useful Kaggle-specific infrastructure from the original project while removing most generic competitive-ML instructions from the root skill.

The design goal is simple: let the model reason about the competition itself, and use the skill for Kaggle-specific execution knowledge, tools, references, submission mechanics, and debugging.

## What changed

The original skill bundled a detailed default competition workflow into `SKILL.md`: task classification, fold design, baseline order, OOF requirements, modeling priorities, escalation rules, ensembling, and submission behavior.

That can be useful for weaker or less autonomous agents, but it can over-constrain stronger models when the competition does not fit the default recipe. ARC-style tasks, unusual code competitions, leaderboard endgames, and competition-specific heuristics are obvious examples.

The Astra-slim version therefore follows three rules:

1. **Keep the root skill small.** `SKILL.md` mainly decides which reference to load and what Kaggle-specific constraints matter.
2. **Load detailed guidance only when relevant.** Validation, tabular modeling, image/text workflows, ensembling, code-competition pipelines, and submission debugging remain available under `references/`.
3. **Match completion to the user's request.** Analysis tasks stop at analysis; implementation tasks stop after implementation/checks; only explicit end-to-end runs are required to continue through Kaggle submission and score retrieval.

## Scope

Use this skill when a task requires Kaggle-specific infrastructure or execution, including:

- Kaggle kernels/notebooks and remote GPU execution;
- Kaggle datasets and artifact handoff;
- code-competition hidden reruns;
- producer/consumer notebook pipelines;
- submission creation and score retrieval;
- debugging failed, timed-out, OOM, or vaguely rejected submissions;
- competition-specific public notebook/discussion reconnaissance when it can materially affect the approach.

A generic ML question, model brainstorm, or offline dataset analysis does not need this skill merely because the dataset came from Kaggle.

## Repository layout

```text
agentic-kaggle-skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── competition-intel.md
│   ├── information-sharing-policy.md
│   ├── cross-validation-and-metrics.md
│   ├── tabular-workflow.md
│   ├── image-text-workflow.md
│   ├── kaggle-code-competition-pipeline.md
│   ├── advanced-notebook-architecture.md
│   ├── kaggle-offload.md
│   ├── kaggle-pipeline-datasets.md
│   ├── submission-endgame.md
│   ├── code-competition-debugging.md
│   ├── ensembling-and-reproducibility.md
│   ├── method-map.md
│   └── research/
├── scripts/
│   ├── scaffold_competition.py
│   ├── make_folds.py
│   ├── prepare_kaggle_kernel.py
│   └── prepare_kaggle_dataset.py
├── examples/
├── requirements.txt
└── LICENSE
```

## Installation

For a user-level Codex skill:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/Jason-W507/agentic-kaggle-skill.git \
  ~/.agents/skills/agentic-kaggle-skill
```

For repo-scoped use, place or symlink the skill under the target repository's `.agents/skills/` directory.

Repo-scoped installation is preferable when Kaggle behavior should not affect unrelated projects.

## Included helpers

The fork preserves the deterministic utility scripts from the upstream project:

- `scripts/scaffold_competition.py` — create a competition workspace;
- `scripts/make_folds.py` — generate reusable fold assignments when folds are actually appropriate;
- `scripts/prepare_kaggle_kernel.py` — prepare Kaggle kernel metadata/layout;
- `scripts/prepare_kaggle_dataset.py` — prepare versioned private artifact datasets.

## Design notes

Detailed references remain available because the point of slimming is not to delete useful Kaggle knowledge. The change is in **when** that knowledge enters context.

Examples:

- A code competition can load the hidden-rerun and artifact-pipeline references without also forcing a tabular baseline recipe.
- A final leaderboard push can use competition intelligence and submission tooling without first rebuilding a classical baseline.
- A normal supervised competition can still load validation, tabular/image/text, and ensembling references when those are useful.

The root skill deliberately avoids universal rules such as “always start with LightGBM,” “always produce OOF predictions,” “always change one thing at a time,” or “every Kaggle task must end with a live submission.” Those are situational decisions.

## Attribution

This repository is a fork of [FrankS-IntelLab/agentic-kaggle-skill](https://github.com/FrankS-IntelLab/agentic-kaggle-skill) and preserves its MIT license and the majority of its reference material and helper scripts.

The Astra-slim refactor changes skill routing, triggering, and completion behavior while retaining the upstream project's Kaggle-specific operational knowledge.

## License

MIT. See `LICENSE`.

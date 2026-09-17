# Kaggle Competition Engineering

A focused Kaggle engineering skill for capable coding agents such as GPT-6 Astra.

This fork is intentionally complementary to [NVIDIA/nvidia-kaggle](https://github.com/NVIDIA/nvidia-kaggle): NVIDIA's plugin handles Kaggle platform operations, while this skill concentrates on complex competition engineering.

## Division of responsibility

Use `nvidia-kaggle-skill` for:

- competition overview, rules, datasets, timelines;
- public writeups, discussions, and kernel research;
- downloading/reproducing public kernels;
- ordinary kernel push/poll/submit workflows;
- submission quota/history;
- Kaggle dataset uploads.

Use `kaggle-competition-engineering` for:

- code competitions and hidden reruns;
- producer/consumer notebook architectures;
- durable model/feature artifact datasets;
- validation and metric design when it materially affects the solution;
- advanced multi-model or multi-stage architectures;
- OOF-safe ensembling/stacking and reproducibility;
- hidden-run OOM, timeout, path/schema/dependency, and scoring failures.

The root `SKILL.md` is deliberately small. It routes the agent to detailed references only when needed and avoids imposing a generic Kaggle recipe.

## Repository layout

```text
agentic-kaggle-skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── kaggle-code-competition-pipeline.md
│   ├── code-competition-debugging.md
│   ├── kaggle-pipeline-datasets.md
│   ├── advanced-notebook-architecture.md
│   ├── cross-validation-and-metrics.md
│   ├── tabular-workflow.md
│   ├── image-text-workflow.md
│   ├── ensembling-and-reproducibility.md
│   └── information-sharing-policy.md
├── scripts/
│   ├── make_folds.py
│   ├── prepare_kaggle_kernel.py
│   └── prepare_kaggle_dataset.py
├── requirements.txt
└── LICENSE
```

## Installation

For Codex, this skill is best installed at repo scope for an active Kaggle project so it does not compete with the broader NVIDIA plugin in unrelated work.

```bash
mkdir -p .agents/skills
git clone https://github.com/Jason-W507/agentic-kaggle-skill.git \
  .agents/skills/kaggle-competition-engineering
```

If both skills are installed, their intended boundary is:

```text
NVIDIA nvidia-kaggle
    Kaggle platform/API/client operations

kaggle-competition-engineering
    competition architecture + validation + artifact engineering + hidden-run robustness
```

## Design principles

- Let GPT-6 Astra reason about the competition instead of following a fixed baseline recipe.
- Load detailed modeling/validation guidance only when the task requires it.
- Keep platform operations separate from architecture decisions.
- Treat producer outputs as versioned contracts with explicit schemas and manifests.
- Design code-competition inference for hidden reruns from the beginning.
- Do not turn analysis or implementation tasks into leaderboard submissions unless the user asked for that execution.

## Included helpers

- `scripts/make_folds.py` — reusable fold assignments when folds are appropriate.
- `scripts/prepare_kaggle_kernel.py` — prepare kernel metadata/layout for engineered pipelines.
- `scripts/prepare_kaggle_dataset.py` — prepare versioned private artifact datasets.

## Attribution

Forked from [FrankS-IntelLab/agentic-kaggle-skill](https://github.com/FrankS-IntelLab/agentic-kaggle-skill). The refactor preserves useful competition-engineering references and helper scripts while removing platform workflows that overlap with NVIDIA's Kaggle plugin.

MIT license. See `LICENSE`.

# Agentic Kaggle Skill

Reusable AI-agent workflow for helping with Kaggle competitions from project setup through validation, modeling, Kaggle execution, debugging, ensembling, and scored submission.

This repository keeps one canonical skill identity:

```yaml
name: agentic-kaggle-skill
```

The skill is written in the open agent skills format so it can be used by multiple agents. Codex-specific metadata lives in `agents/openai.yaml`; Hermes users can consume the same root `SKILL.md` and bundled resources.

## Supported Agents

| Agent | Status | Notes |
| --- | --- | --- |
| Codex | First-class | Uses `SKILL.md`, `agents/openai.yaml`, `references/`, and `scripts/`. |
| Hermes | Supported | Use the same skill folder. Hermes-specific examples remain in `references/research/`. |

## What It Does

- Reads Kaggle rules, data terms, metric, submission format, and scoring mode before modeling.
- Builds metric-correct baselines with stable folds and out-of-fold predictions.
- Uses public notebook and discussion intelligence as scouting signals, not copied source.
- Offloads heavy work to Kaggle notebooks/scripts when local compute is insufficient.
- Supports staged producer/consumer notebook pipelines with private artifact datasets.
- Handles code-competition hidden rerun failures, vague scoring errors, timeouts, and OOMs.
- Tracks reproducibility artifacts, run logs, score receipts, and ensemble evidence.
- Continues toward a scored Kaggle submission or records a concrete blocker.

## Install

### Codex

Install as a user-level Codex skill:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/FrankS-IntelLab/agentic-kaggle-skill.git \
  ~/.agents/skills/agentic-kaggle-skill
```

Restart Codex if the skill does not appear immediately. Invoke it explicitly with:

```text
Use $agentic-kaggle-skill to help me start this Kaggle competition.
```

For repo-scoped development, place or symlink this folder under a repository's `.agents/skills/` directory:

```bash
mkdir -p .agents/skills
ln -s /path/to/agentic-kaggle-skill .agents/skills/agentic-kaggle-skill
```

### Hermes

Install the whole skill folder so references and scripts are available:

```bash
mkdir -p ~/.hermes/skills/data-science
git clone https://github.com/FrankS-IntelLab/agentic-kaggle-skill.git \
  ~/.hermes/skills/data-science/agentic-kaggle
```

Then ask Hermes to use the agentic Kaggle skill for competition work.

### Helper Script Dependencies

Most scripts use only the Python standard library. `scripts/make_folds.py` requires pandas and numpy; scikit-learn is recommended for standard splitters.

```bash
python3 -m pip install -r requirements.txt
```

## Repository Layout

```text
agentic-kaggle-skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── method-map.md
│   ├── information-sharing-policy.md
│   ├── competition-intel.md
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
│   └── research/
├── scripts/
│   ├── scaffold_competition.py
│   ├── make_folds.py
│   ├── prepare_kaggle_kernel.py
│   └── prepare_kaggle_dataset.py
├── examples/
│   ├── rl-game-case-study.md
│   └── audio-classification-case-study.md
├── requirements.txt
├── README.md
└── LICENSE
```

## Design Notes

`SKILL.md` is the canonical entry point. It stays concise and tells the agent which reference file to load for each Kaggle workflow.

`agents/openai.yaml` is Codex-facing UI metadata. It does not fork the workflow; it only improves how the skill appears and is invoked in Codex.

`references/` contains detailed workflow guidance loaded only when relevant. The `references/research/` folder preserves earlier Hermes-era lessons, troubleshooting notes, automation patterns, and case-specific insights.

`scripts/` contains repeatable utilities for scaffolding a Kaggle project, making folds, preparing Kaggle kernels, and preparing private Kaggle artifact datasets.

## Attribution And Safety

This skill is source-agnostic. It packages general competitive ML and Kaggle workflow procedures rather than copying named public notebooks, books, or papers.

When using public notebooks or discussions during an active competition, treat them as scouting signals. Do not copy code, text, model artifacts, generated features, or data-derived outputs without checking the competition rules, data license, third-party license obligations, and attribution requirements.

## Development

Keep the public identity aligned everywhere:

```text
agentic-kaggle-skill
```

When updating the skill:

1. Keep the canonical workflow in `SKILL.md`.
2. Put detailed procedure in `references/`.
3. Put deterministic helpers in `scripts/`.
4. Regenerate or update `agents/openai.yaml` when the skill name, scope, or default prompt changes.
5. Validate the skill metadata before release.

## License

MIT. See `LICENSE`.

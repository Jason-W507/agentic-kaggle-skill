---
name: agentic-kaggle-skill
description: Execute Kaggle-specific workflows such as kernels, datasets, code-competition pipelines, submissions, score retrieval, and submission debugging. Use when the task requires Kaggle infrastructure or competition-specific execution.
---

# Agentic Kaggle Skill

Use this skill for Kaggle-specific execution. Keep strategy adaptive to the competition and the user's objective; do not impose a generic modeling recipe when the task does not require one.

## Route by task

Load only the references that are relevant:

- `references/competition-intel.md` — public notebooks/discussions may materially inform the current competition.
- `references/information-sharing-policy.md` — before publishing or redistributing competition-derived code, data, models, or artifacts.
- `references/kaggle-code-competition-pipeline.md` — code competitions, hidden reruns, final scoring notebooks, producer/consumer handoffs.
- `references/code-competition-debugging.md` — failed, timed-out, OOM, or vaguely rejected code-competition submissions.
- `references/kaggle-offload.md` — remote Kaggle GPU/TPU execution or Kaggle-only data access.
- `references/kaggle-pipeline-datasets.md` — durable intermediate/model artifacts passed between notebooks.
- `references/submission-endgame.md` — only when the user wants an end-to-end run through actual submission/scoring.
- `references/cross-validation-and-metrics.md` — when validation design, leakage, thresholds, or metric reproduction matter.
- `references/tabular-workflow.md`, `references/image-text-workflow.md`, `references/advanced-notebook-architecture.md`, `references/ensembling-and-reproducibility.md` — only when those techniques are relevant to the current competition.
- `references/method-map.md`, `references/research/`, and `examples/` — background or historical context when useful, not default prerequisites.

## Execution principles

- First determine what the user actually wants: analysis, implementation, remote execution, debugging, or scored submission.
- Inspect competition rules, scoring mode, metric, submission format, and environment constraints when they affect the requested work.
- Use live competition intelligence when it is likely to change the approach; do not scan public solutions mechanically for every task.
- Let the competition structure determine the modeling and validation strategy. Do not assume that folds, OOF predictions, a classical baseline, one-change-at-a-time iteration, or ensembling are always appropriate.
- Reuse the bundled scripts when they save deterministic setup work:
  - `scripts/scaffold_competition.py`
  - `scripts/make_folds.py`
  - `scripts/prepare_kaggle_kernel.py`
  - `scripts/prepare_kaggle_dataset.py`
- For code competitions, design around hidden reruns and immutable attached artifacts rather than local-only paths or implicit upstream state.
- Keep competition data, credentials, private datasets, checkpoints, submissions, and restricted artifacts out of public repositories unless the rules and licenses permit publication.

## Completion behavior

Match the stopping point to the user's request.

- For analysis or planning tasks, stop when the requested analysis or plan is complete.
- For implementation tasks, continue through the requested implementation and checks.
- For end-to-end competition execution, continue through Kaggle submission and retrieve the resulting status/score, or document a concrete external blocker. Use `references/submission-endgame.md` for that case.
- When a submission fails for a fixable technical reason, debug and retry rather than treating the first failure as final.

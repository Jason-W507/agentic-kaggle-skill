---
name: kaggle-competition-engineering
description: Design and debug complex Kaggle competition systems: code competitions, producer/consumer pipelines, artifact datasets, validation, ensembling, and hidden-rerun robustness. Use for competition engineering, not Kaggle browsing, public-kernel discovery/reproduction, ordinary submissions, or dataset uploads.
---

# Kaggle Competition Engineering

Use this skill for the engineering layer of a Kaggle solution. Keep competition strategy adaptive to the task and load only the references that are relevant.

This skill is intentionally complementary to `nvidia-kaggle-skill`. When that skill is available, prefer it for Kaggle platform operations such as competition overview, writeups/discussions, public-kernel research or reproduction, ordinary push/submit/poll workflows, submission quota/history, and dataset uploads.

## Route by task

- `references/kaggle-code-competition-pipeline.md` — code competitions, hidden reruns, final scoring notebooks, producer/consumer handoffs.
- `references/code-competition-debugging.md` — hidden-rerun failures, OOMs, timeouts, schema/path/dependency failures, and vague scoring errors.
- `references/kaggle-pipeline-datasets.md` — durable model/feature artifacts passed between producer and consumer notebooks.
- `references/advanced-notebook-architecture.md` — staged multi-model or multi-notebook architectures when a single notebook is insufficient.
- `references/cross-validation-and-metrics.md` — validation design, leakage, thresholds, and metric reproduction when those questions matter.
- `references/tabular-workflow.md` — tabular-specific modeling guidance when relevant.
- `references/image-text-workflow.md` — image, segmentation, or text-specific modeling guidance when relevant.
- `references/ensembling-and-reproducibility.md` — OOF-safe blending/stacking and experiment reproducibility.
- `references/information-sharing-policy.md` — before publishing or redistributing competition-derived artifacts.

## Engineering principles

- Let the competition structure determine validation and modeling. Do not assume folds, OOF predictions, classical baselines, ensembling, or one-change-at-a-time iteration are universally appropriate.
- For code competitions, design explicitly for hidden reruns: immutable attached artifacts, deterministic paths, bounded memory/runtime, and no implicit upstream state.
- Treat producer outputs as versioned contracts. Record model/config/schema/fold metadata needed by downstream consumers.
- Separate architecture decisions from platform operations. This skill should decide what to build and how stages fit together; use Kaggle tooling or `nvidia-kaggle-skill` for routine platform-facing actions when available.
- Reuse the bundled deterministic helpers when useful:
  - `scripts/make_folds.py`
  - `scripts/prepare_kaggle_kernel.py`
  - `scripts/prepare_kaggle_dataset.py`
- Keep competition data, credentials, private datasets, checkpoints, submissions, and restricted artifacts out of public repositories unless rules and licenses permit publication.

## Completion behavior

Match the stopping point to the user's request. Complete the requested design, implementation, artifact pipeline, validation work, or debugging. Do not independently expand the task into public-solution research or routine leaderboard submission merely because the work is on Kaggle.

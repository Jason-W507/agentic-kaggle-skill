# Submission Endgame

Use this reference only when the user wants the Kaggle task carried through actual submission/scoring, or when the current task explicitly includes submission, leaderboard score retrieval, or debugging a scoring failure.

Do not force every Kaggle analysis, planning, or implementation task into a live submission.

Before publishing final code, reports, models, or artifacts outside the team, read `information-sharing-policy.md`.

## End Condition

For end-to-end execution, continue until one of these states is reached:

- `scored`: Kaggle accepted and processed the requested submission, and the submission status plus public score or visible scoring result has been retrieved.
- `blocked`: an external condition prevents scoring, such as missing Kaggle credentials, competition rules not accepted, submission quota exhausted, competition closed, scoring disabled, required manual UI-only action, missing kernel version, or Kaggle service failure.

A fixable implementation or code-competition failure is not an external blocker. When appropriate, read `code-competition-debugging.md`, patch defensively, rerun/resubmit, and retrieve the new result.

If blocked, record the exact error or condition, the artifact that is ready, and the next action needed.

## Classic Submission Flow

For ordinary competitions where a prediction file is accepted:

```bash
kaggle competitions submit COMPETITION_SLUG -f SUBMISSION_FILE -m "RUN_ID_OR_MESSAGE"
kaggle competitions submissions COMPETITION_SLUG -v -q
```

Before submitting, verify only the conditions relevant to the competition: file existence and schema, row/ID alignment, value format, credentials/rules acceptance, and any competition-specific constraints.

After submitting, retrieve the processed status/score and record enough metadata to identify the submitted artifact and run.

## Code Competition Or Final Notebook Flow

For code competitions or notebook-scored workflows:

1. Ensure required upstream artifacts are available and stable.
2. Push/run the final scoring notebook or script.
3. Retrieve its outputs and verify the scoring artifact.
4. Submit the required file or kernel/version according to the competition mechanism.
5. Retrieve submission status/score.
6. If scoring fails for a technical reason, use `code-competition-debugging.md` and retry when a concrete fix is available.

For multi-stage pipelines, durable model/feature artifacts should be attached explicitly rather than depending on rerunning upstream notebooks during hidden scoring. See `kaggle-code-competition-pipeline.md` and `kaggle-pipeline-datasets.md` when relevant.

## Final Run Summary

For an end-to-end run, report the information that materially identifies the result, such as:

- competition slug/title;
- final file or kernel/version;
- run or artifact reference;
- submission status and public score when available;
- any relevant local validation evidence;
- debugging outcome or concrete blocker if scoring did not complete.

Do not manufacture fields that do not exist for the competition or force a generic experiment schema onto unusual competitions.

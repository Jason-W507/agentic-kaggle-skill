# Competition Intelligence

Use this reference when current public Kaggle notebooks, discussions, leaderboard context, or rule clarifications are likely to change the requested analysis or implementation.

Do not scan public material mechanically for every Kaggle task. Match the depth of scouting to the user's goal, competition stage, and uncertainty.

Before reusing or publishing material derived from public competition resources, read `information-sharing-policy.md`.

## Sources

When available, use Kaggle competition-intelligence tools, Kaggle UI/API/CLI, or user-provided public links to inspect relevant notebooks and discussions.

Focus on signals that can materially affect the work:

- competition-specific validation or hidden-test structure;
- scoring or submission mechanics;
- data quirks, bugs, leakage warnings, and rule clarifications;
- strong public baselines or newly shared methods;
- inference/runtime constraints for code competitions;
- leaderboard behavior that may indicate public-LB overfitting or distribution shift.

Treat public solutions as evidence and ideas, not authority. Do not assume that a popular notebook is optimal for the current objective, and do not copy restricted code, artifacts, or data without checking rules and licenses.

## Scouting depth

Choose the smallest useful search:

- For a narrow question, inspect only the directly relevant public sources.
- Before an expensive architectural decision, compare several strong and recent public approaches plus high-signal discussions.
- During a fast-moving endgame, weight recency and leaderboard evidence more heavily while still distinguishing public-LB gains from robust evidence.
- When the user already supplied a baseline or specific public notebook, start from that context instead of re-running broad generic scouting.

Avoid fixed quotas such as always reading exactly five notebooks or five discussions. Increase breadth only when the first pass leaves an important uncertainty unresolved.

## Extract actionable evidence

Summarize the parts that affect decisions, for example:

- technique or architecture;
- validation/testing evidence;
- public score and timing when relevant;
- runtime/resource profile;
- competition-specific implementation details;
- known failure modes or rule constraints;
- why the idea is or is not worth testing in the user's current setup.

Separate observed facts from your inference. Flag methods that appear dependent on leakage, fragile public-LB tuning, unavailable external data, or prohibited sharing.

## Fallback

If live Kaggle intelligence is unavailable, use existing local notes, public writeups, user-provided links, or proceed from the competition specification and available code. State the limitation only when it materially affects confidence in the recommendation.

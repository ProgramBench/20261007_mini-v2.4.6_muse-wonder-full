# Muse Wonder Full — ProgramBench submission

- **Model:** Muse Wonder Full, max 65,536 output tokens per call. 188 tasks were run on the
  model's dedicated endpoint and 12 through an API-served endpoint.
- **Scaffold:** mini-SWE-agent v2.4.5–2.4.6 (single-agent), open source; step limit 1,000, no cost
  limit, 48 h wall-time limit
- **Protocol:** no-internet + `task_cleanroom_v6` images. The agent sees only the compiled binary
  (source removed, `.git` reset), reimplements it from scratch by interacting with it, and never
  has network access (`--network none` at the container level).
- **Score:** ~0.885 (mean per-instance test pass-rate over the fixed 200; the leaderboard
  recomputes authoritatively from `_stats/score.json`). Only tests listed in the benchmark's
  `tests.json` are scored.
- **Inference dates:** 2026-10-07 to 2026-10-09

## Task accounting

All 200 tasks are evaluated and included. Rollouts that hit the context limit without
submitting had their final workspace evaluated as-is.

## Extra stats

Model-call and output-token statistics are generated from the published trajectories by the
scripts under `_scripts/`.

## Redactions

Plaintext reasoning (`reasoning_content`) is removed from every trajectory; the opaque
`reasoning_id`s are kept. Harness metadata naming internal hosts and users is replaced with
`[REDACTED]` in each trajectory's `info.config` (`litellm_model_registry`, `output_path`), host
paths in harness tracebacks are rewritten to `/harness/`, and credential fields in the harness
config are replaced with `[REDACTED]`. Model and tool turns are otherwise unmodified.

Each test is run up to 3× (pytest-rerunfailures); only the final attempt is scored (flakiness defense).

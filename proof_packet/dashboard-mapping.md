# Dashboard Mapping

This note maps the current Evidential bandit analysis response into a dashboard that a nonprofit program team can use.

## Backend Field Mapping

| Backend Field | Dashboard Use |
| --- | --- |
| `experiment_id` | Experiment title/subtitle and audit reference. |
| `type` | Shows this is a bandit result view. |
| `n_outcomes` | Low-data warning and confidence context. |
| `created_at` | Analysis timestamp. |
| `contexts` | Contextual-analysis badge when present. |
| `arm_analyses[].arm_id` | Stable arm identifier for audit rows. |
| `arm_analyses[].arm_name` | Arm result card title. |
| `arm_analyses[].post_pred_mean` | Expected outcome on the result card. |
| `arm_analyses[].post_pred_ci_lower` | Lower uncertainty interval. |
| `arm_analyses[].post_pred_ci_upper` | Upper uncertainty interval. |
| `arm_analyses[].prior_pred_mean` | Prior expectation, useful for change-from-prior display. |
| assignment counts from logs | Allocation share over time. |
| reward counts from logs | Observed reward rate. |
| policy metadata | Replay/audit table. |

## Dashboard Sections

### Experiment Summary

Show the current leader, total outcomes, analysis timestamp, and caution status.

### Arm Results

Each arm card shows expected outcome, uncertainty interval, observed rate, assignment share, and a status label:

- `Needs more data`
- `Leading but uncertain`
- `Stable leader`
- `Watch guardrails`

### Allocation Over Time

Show how allocation changed across synthetic rounds. This makes adaptive allocation inspectable instead of opaque.

### Replay / Audit Trail

Show a short table of policy decisions: round, selected arm, context, reason, and outcome. This is the proof slice for future replay work.

### How This Maps To Evidential

State which fields come from current backend response models and which fields require assignment-log aggregation or new metadata.

## Proposed Product Principle

Do not make the first dashboard screen a statistics dump. Show the decision state first, then expose posterior and allocation details for inspection.

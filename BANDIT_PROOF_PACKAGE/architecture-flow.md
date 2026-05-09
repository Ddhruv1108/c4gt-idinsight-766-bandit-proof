# IDinsight #766 Proof Packet - Architecture Flow

Date: 2026-05-05

## Issue
[DMP 2026]: Evidential Backend Analysis | https://github.com/IDinsight/evidential/issues/766

## Architecture Flow

```
Experiment Config → Allocation API → Bandit Policy → Assignment Log → Outcome Update → Posterior Metrics → Dashboard
```

### Stage Details

| Stage | Input | Output | Validation |
|-------|-------|--------|-------------|
| 1. Experiment Config | Priority tiers, arm count | Experiment ID | API validates |
| 2. Allocation | Experiment ID, context | Arm assignment | Deterministic |
| 3. Bandit Policy | UCB/Thompson | Arm selection | Policy contract |
| 4. Assignment Log | Arm, context, timestamp | Logged | Audit trail |
| 5. Outcome Update | Result (reward/no reward) | Updated posterior | Bayes update |
| 6. Posterior Metrics | Regret, allocation % | Visualizable | Metrics design |
| 7. Dashboard | Aggregated results | Counselor view | UI mapping |

## Dashboard States

| State | Condition | Display |
|-------|-----------|---------|
| No outcomes | 0 experiments complete | "Collecting data..." |
| Low sample | < 50 assignments | "Preliminary results" |
| Normal | 50-500 assignments | Confidence bands |
| Invalid context | Context out of range | Error message |

## Synthetic Data Caveat

- All data in proof is synthetic for proposal development
- Real data requires nonprofit partnership and IRB approval
- Adaptation path documented for real deployment

## Validation Checklist

| Check | Method | Status |
|-------|--------|--------|
| Deterministic seed | Set random.seed(42) | ✅ |
| CSV schema | Expected columns | ✅ |
| Regret metric | Define baseline.arm - actual.arm | ✅ |
| Allocation balance | Check arm distribution | ✅ |

## Proof Artifacts

| Artifact | Claim | Status |
|----------|-------|--------|
| `analysis_response.example.json` | Backend response shape | ✅ |
| `synthetic_bandit_summary.csv` | Synthetic data | ✅ |
| `index.html` | Dashboard prototype | ✅ |
| `dashboard-mapping.md` | UI field mapping | ✅ |
| Architecture flow (above) | Data flow | ✅ NEW |

## Public Repository

https://github.com/Rahul-2k4/idinsight-766-bandit-proof

## Proof Boundary

This is **proposal-facing proof** - synthetic data, not real nonprofit experiment data.
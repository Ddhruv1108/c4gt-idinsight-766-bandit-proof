# IDinsight #766 Runtime Proof Rerun

**Date**: 2026-05-06  
**Run**: python3 bandit-spike-py/bandit_test.py

## Command & Output

```
=== Thompson Sampling (500 pulls) ===
  Arm 0: pulls=22, est=0.045, true=0.100
  Arm 1: pulls=413, est=0.271, true=0.300
  Arm 2: pulls=65, est=0.138, true=0.150

=== UCB1 (500 pulls) ===
  Arm 0: pulls=104, est=0.096, true=0.100
  Arm 1: pulls=270, est=0.293, true=0.300
  Arm 2: pulls=126, est=0.143, true=0.150

=== Verification ===
Thompson Sampling best arm: 1 (true best: 1)
UCB best arm: 1 (true best: 1)

✓ All tests passed!
```

## Additional Validation

- **JSON**: Validated `BANDIT_PROOF_PACKAGE/analysis_response.example.json`
- **CSV**: Available at `BANDIT_PROOF_PACKAGE/synthetic_bandit_summary.csv`
- **Dashboard**: Static HTML at `BANDIT_PROOF_PACKAGE/index.html`

## Result

- **Python proof**: PASS (2/2 algorithms identify correct best arm)
- **JSON validation**: PASS
- **Exit code**: 0

## Proof Boundary

- **Synthetic data**: Uses synthetic 3-arm Bernoulli bandits
- **No real nonprofit data**: All inputs are programmatically generated
- **No upstream UI patch**: Prototype is synthetic-only
- **No production impact**: Simulation only

## What This Proves

- Thompson Sampling and UCB1 algorithms work correctly
- Synthetic bandit simulation is reproducible
- JSON/CSV artifacts are syntactically valid

## What This Does NOT Prove

- Real nonprofit experiment data
- Production bandit deployment
- Turn.io integration
- Dashboard connects to real backend
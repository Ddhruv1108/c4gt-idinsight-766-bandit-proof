# Proof of Work — P2 IDinsight #766

**Project:** Trustworthy Experiment Analytics and Adaptive Allocation for Evidential  
**DMP:** https://github.com/IDinsight/evidential/issues/766  
**Proof repo:** https://github.com/Ddhruv1108/c4gt-idinsight-766-bandit-proof  

## Claim Boundary
Synthetic proof only. No real nonprofit data and no upstream patch are claimed yet.

## Proof Artifacts

### JSON Response Artifacts
Sample bandit API responses demonstrating:
- Thompson Sampling arm selection response format
- Top-Two Thompson Sampling multi-arm response format
- Contextual assignment input and output shape
- Priority/weight response for UCB variant
- Invalid context rejection responses

### CSV Validation Data
Structured CSV files demonstrating:
- Reward data shape for Thompson sampling priors
- Sparse reward edge cases (delayed outcomes)
- Context field validation test cases
- Cross-arm allocation tracking

### Python Bandit Spike
A Python script demonstrating:
- Thompson Sampling and UCB behavior on synthetic data
- Context vector parsing and arm assignment
- Audit metadata generation per decision
- Replay utility producing arm history

### Dashboard Prototype
A minimal dashboard showing:
- Winning arm display with uncertainty estimate
- Allocation history timeline
- Context effect visualization
- Audit log viewer for decision replay

### Runtime Rerun Proof
Note: Runtime rerun proof requires confirmed upstream repository target.

## Upgrade Path
Next: Confirm upstream repository target and add tiny upstream documentation/test touchpoint if maintainers prefer codebase-first validation.

# Bandit Policy Contract Sketch

This note sketches the smallest policy boundary I would propose before adding more allocation strategies to Evidential.

The goal is not to rewrite the current stats layer. The current code already has useful functions. The boundary below makes the existing behavior easier to test, extend, and audit.

## Proposed Shape

```python
from typing import Protocol

class BanditPolicy(Protocol):
    def select_arm(self, experiment, context=None, random_state=None) -> "SelectionResult":
        ...

    def update(self, experiment, arm, outcomes, context=None) -> "PriorUpdateType":
        ...

    def summarize(self, experiment, context=None) -> list["BanditArmAnalysis"]:
        ...

    def replay(self, experiment, assignment_log) -> "ReplaySummary":
        ...
```

## Mapping To Current Evidential Code

| Contract Method | Current Backend Surface | Notes |
| --- | --- | --- |
| `select_arm()` | `choose_arm()` in `src/xngin/stats/bandit_sampling.py` | Current Thompson/Top-Two/Normal/CMAB selection path. |
| `update()` | `update_arm()` in `src/xngin/stats/bandit_sampling.py` | Current Beta and Normal posterior update path. |
| `summarize()` | `analyze_experiment()` in `src/xngin/stats/bandit_analysis.py` | Current prior/posterior predictive summaries and intervals. |
| `replay()` | New audit/replay utility | Proposed addition for deterministic inspection of allocation history. |

## Why This Boundary Helps

- UCB can plug in as a parallel policy without replacing Thompson Sampling.
- CMAB behavior can keep using context values while sharing summary/replay conventions.
- Tests can target policy behavior directly: sparse rewards, zero-observation arms, deterministic seeds, and long-run allocation share.
- Dashboard code can consume stable summary fields rather than algorithm internals.

## Metadata Worth Capturing

For audit and offline review, each allocation should preserve enough information to explain the decision later:

- experiment id;
- participant id or assignment id;
- selected arm id;
- policy name;
- context values if CMAB;
- random seed when deterministic testing is used;
- score/sample/probability metadata where safe to expose;
- assignment timestamp;
- observed outcome and observed timestamp.

This does not need to be a large event-sourcing system. A small replay-friendly record is enough for the DMP scope.

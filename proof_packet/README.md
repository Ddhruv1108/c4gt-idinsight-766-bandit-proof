# IDinsight #766 Bandit Results Proof

This is a small proposal proof for C4GT DMP 2026 issue #766: IDinsight Experiment Analytics & Bandits Engine Enhancements.

It is not upstream Evidential code. It is a reviewer-checkable prototype that shows how the current Evidential bandit analysis surface can become a dashboard and replay view for nonprofit teams.

## What This Proves

- The proposal is grounded in the existing Evidential backend, not a separate ML demo.
- Bandit results can be shown without exposing raw statistical internals first.
- A compact policy boundary can support Thompson Sampling, UCB, contextual bandits, and replay/audit metadata.
- The dashboard can stay close to fields already present in or adjacent to `BanditExperimentAnalysisResponse` and `BanditArmAnalysis`.

## Demo Scenario

The synthetic example is a nonprofit education program testing WhatsApp homework reminders:

- Current reminder
- Motivational reminder
- Parent prompt

The reward is homework completion. The values are intentionally small because nonprofit experiments often have sparse or delayed outcome data.

## Files

- `index.html`: static mi-fi dashboard prototype.
- `analysis_response.example.json`: Evidential-shaped bandit analysis payload.
- `synthetic_bandit_summary.csv`: synthetic allocation and reward summary.
- `dashboard-mapping.md`: backend-to-dashboard field mapping.
- `policy-contract.md`: proposed policy boundary mapped to existing backend functions.
- `selection-patterns.md`: why this proof is shaped like accepted C4GT/GSoC proposals.
- `contextual_example_table.md`: user-level context vectors and expected CMAB arm preference shifts.

## How To View

Open `index.html` in a browser. It has no build step and no external dependencies.

Optional local server view:

`python3 -m http.server 8012` then open `http://127.0.0.1:8012/`.

## Screenshot Evidence

These PNG files are included under `screenshots/`:

- `01-summary-cards.png`: top summary cards (experiment, leader, outcomes, policy).
- `02-arm-results.png`: arm cards with posterior means, intervals, and assignment share bars.
- `03-allocation-table.png`: allocation-over-time table with regret column.
- `04-audit-trail.png`: replay/audit trail table.

Captions:

- `Summary view with leader status and policy context`
- `Arm-level uncertainty and allocation behavior`
- `Allocation shift over rounds with regret tracking`
- `Replay/audit event log for decision transparency`

## Synthetic Method Notes

- Arm-level posterior means/intervals are synthetic values shaped like `BanditExperimentAnalysisResponse` fields.
- Allocation table percentages are synthetic round snapshots for 50/100/200/500 assignment rounds.
- `Regret vs oracle` is a synthetic sanity metric for relative allocation quality in this toy setup. It is included for reviewer discussion, not as production accuracy evidence.
- Audit events are synthetic checkpoints to show replay/audit schema design, not logs from production traffic.

## What This Is Not

- Not a merged upstream feature.
- Not a replacement for Evidential's current Thompson/CMAB implementation.
- Not proof of real-world program impact.
- Not a claim that UCB should replace the existing Bayesian path.

The intended claim is narrower: the proposal has a concrete implementation direction, an inspectable product surface, and codebase-specific reasoning behind it.

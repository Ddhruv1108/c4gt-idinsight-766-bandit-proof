Hi @markbotterill @poornimaramesh,

I reviewed the Evidential backend around the bandit flow before finalizing my proposal. From the public repo, it looks like `bandit_sampling.py` already supports Thompson Sampling, Top-Two Thompson Sampling, Beta/Normal prior paths, and CMAB-style context-aware selection. `bandit_analysis.py` and `BanditExperimentAnalysisResponse` also seem to expose enough posterior summary data for a first dashboard pass.

To make my proposal less hand-wavy, I made a small proof package that maps an Evidential-shaped bandit analysis response into a dashboard/replay view:

`[link TBD once public]`

This is a prototype, not upstream code. The goal is to make the scope concrete: preserve the current Thompson/CMAB paths, add UCB only if that is still useful, tighten context validation, and expose allocation, uncertainty, and replay metadata in the results view.

A few scope questions before I submit:

1. Is `agency-fund/evidential-be` the canonical repo for this DMP work?
2. For midpoint, would you prefer UCB as a new policy, or hardening the current Thompson/Top-Two/CMAB paths with dashboard/replay support?
3. For contextual bandits, should user-level features come from request-time assignment context, warehouse participant fields, or both?
4. Should replay/audit metadata include action probabilities, or should the first version keep only policy name, context, selected arm, timestamp, and outcome?

Thanks.

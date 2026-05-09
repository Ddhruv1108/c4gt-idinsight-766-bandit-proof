# Prior-Year Proposal Patterns Applied

Accepted C4GT and GSoC-style proposals consistently show:

- precise project understanding, not generic definitions;
- mentor interaction and scope questions;
- proof of ability through PRs, PoCs, examples, tests, screenshots, or demos;
- concrete architecture and milestones;
- required vs optional deliverables;
- test/demo artifacts reviewers can inspect;
- honest scope boundaries and clear stretch goals.

The Cosmic Regolith proposal followed this pattern well: it named exact files and services, showed root-cause analysis, included qualification proof, linked screenshots and a proof repo, and tied the implementation plan to mentor feedback.

This proof package applies the same approach to IDinsight #766:

- It maps the proposed dashboard to existing Evidential backend models.
- It keeps the proof reviewer-checkable through CSV, JSON, markdown, and static HTML.
- It labels the dashboard as a prototype, not upstream UI.
- It turns the proposal's "bandit analytics" idea into a concrete inspectable artifact.
- It generates mentor questions from a real system mapping rather than from generic bandit theory.

The intended reviewer signal: the applicant has already studied the current system and can turn the issue brief into a scoped implementation path.

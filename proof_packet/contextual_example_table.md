# Contextual Bandit Example Table

This table shows a minimal CMAB-style example using user-level features and expected preference shifts. It is a synthetic validation artifact for proposal review.

| Case | Context Vector (user-level features) | Expected Arm Preference | Why |
| --- | --- | --- | --- |
| A | `student_grade=low`, `prior_completion=low`, `parent_phone_available=true` | `parent_prompt` | Parent intervention is likely more effective when completion history is weak and parent contact exists. |
| B | `student_grade=mid`, `prior_completion=mid`, `parent_phone_available=false` | `motivational_reminder` | Motivational nudge likely outperforms parent prompt when parent channel is unavailable. |
| C | `student_grade=high`, `prior_completion=high`, `parent_phone_available=false` | `current_reminder` or `motivational_reminder` close | Baseline may remain competitive when completion risk is already low. |

How this is used in proposal validation:

- Confirm context values are mapped by `context_id`.
- Confirm assignment path changes when context vector changes.
- Confirm replay/audit row records chosen arm and context snapshot.

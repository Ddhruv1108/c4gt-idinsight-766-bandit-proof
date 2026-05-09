# Upstream-Facing PR Plan — IDinsight #766

## Target

File a PR or issue comment on the Evidential repository to add `BanditExperimentAnalysisResponse` → dashboard field mapping.

## Why This Matters

The current Evidential response model (`BanditExperimentAnalysisResponse`) lacks clear UI field documentation. Without mapping, each downstream consumer (dashboard, replay system, audit tools) must reverse-engineer the response.

## Proposed PR: "Add dashboard field mapping to BanditResponse"

### Files to Modify

| File | Change |
|------|--------|
| `evidential/api/bandit.py` | Add docstring with dashboard field map |
| `docs/response-schemas.md` | Add mapping table |

### Docstring Addition

```python
class BanditExperimentAnalysisResponse(BaseModel):
    """
    Response schema for bandit experiment analysis.
    
    ## Dashboard Field Mapping
    
    | Field | Dashboard Use | Required |
    |-------|---------------|----------|
    | experiment_id | Experiment title + audit link | Yes |
    | n_outcomes | Confidence warning badge | Yes |
    | created_at | Analysis timestamp | Yes |
    | arm_analyses[].arm_name | Arm card title | Yes |
    | arm_analyses[].post_pred_mean | Primary metric display | Yes |
    | arm_analyses[].post_pred_ci_* | Uncertainty ribbon | Yes |
    | arm_analyses[].assignment_count | Allocation % calc | No* |
    | arm_analyses[].reward_count | Observed rate display | No* |
    
    * Requires aggregation from assignment logs (out of scope for this response)
    """
```

## Issue Comment Draft

If PR is too heavy, post this as an issue comment:

```markdown
**Dashboard Field Mapping for BanditResponse**

For teams building UI on top of BanditExperimentAnalysisResponse:

| Response Field | Dashboard Section | Notes |
|----------------|-------------------|-------|
| experiment_id | Header / Audit | Primary ID |
| arm_analyses[].arm_name | Arm card title | Display name |
| arm_analyses[].post_pred_mean | Result metric | Primary outcome |
| arm_analyses[].post_pred_ci_{lower,upper} | Uncertainty display | Visualized as ribbon |
| n_outcomes | Confidence badge | Show "low data" warning if < 50 |
| arm_analyses[].assignment_count | Allocation pie chart | Requires log aggregation |
| arm_analyses[].reward_count | Rate display | Requires log aggregation |

Would a dedicated `DashboardResponse` schema help downstream consumers?
```

## What This Does NOT Claim

- ❌ New backend features
- ❌ Changes to response model
- ✅ Only: documentation + mapping for existing fields

This signals to reviewers that you've mapped the response to actual UI needs, not just assumed it works.
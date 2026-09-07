# PRD template

**Template:** Product requirements

## Purpose

Define the problem, goals, scope, and success criteria for a product initiative so the team and stakeholders are aligned.

# Feature Specification: [Feature Name]

## Overview

[2-3 sentence summary of what this feature does and why it exists.]

---

## Goals

- [User-facing goal]
- [Business goal]
- [Technical constraint or non-goal]

---

## Core Concepts

- [Term] = [definition]
- [Assumption or invariant that shapes the design]

---

## Entry Points

### [Screen / Surface Name]

- [UI element added or changed]
- [Trigger condition if non-obvious]

---

## User Flows

### [Flow Name]

**Trigger:** [What initiates this flow]

**Steps:**
1. [Step]
2. [Step]

**Outcome:** [What the user ends up with]

---

## UI Specification

### [Component / Modal / Screen]

**Layout:**
- [Description of structure]

**Elements:**
- [Input / button / label and its behavior]

**States:**
- Default: [description]
- Loading: [description]
- Error: [description]
- Empty: [description]

---

## Permissions

| Capability | [Role A] | [Role B] |
|------------|----------|----------|
| [Action]   | Yes / No | Yes / No |

---

## Edge Cases

| Scenario | Expected behavior |
|----------|-------------------|
| [e.g. expired link] | [Show message X] |
| [e.g. revoked access] | [Redirect to Y] |

---

## Analytics Instrumentation

> These events must be instrumented before the feature ships.
> All events should include base properties: `user_id`, `project_id`, `timestamp`.

| Event name | Trigger | Key properties |
|------------|---------|----------------|
| `[feature]_[action]` | [When it fires] | `[prop_1]`, `[prop_2]` |

**Example:**

| Event name | Trigger | Key properties |
|------------|---------|----------------|
| `chat_share_initiated` | User opens share modal | `share_type` (private/public) |
| `chat_share_completed` | Share is confirmed | `share_type`, `permission_level` |
| `shared_chat_viewed` | Recipient opens shared link | `is_live`, `viewer_type` (owner/invited/public) |

---

## Acceptance Criteria

Criteria are written as testable pass/fail conditions.
Each maps to a user flow or edge case above.

### [Feature Area, e.g. Share Modal]

- [ ] Clicking Share opens the modal within 300ms
- [ ] Private share tab shows email input and permission selector
- [ ] Invite sends email and adds recipient to access list
- [ ] Public link is generated on first toggle and persists on reload

### [Feature Area, e.g. Shared View]

- [ ] Recipient sees read-only chat with no editing controls
- [ ] Recipient cannot navigate to the source project
- [ ] Revoking access causes link to return 403 within 60 seconds

### [Feature Area, e.g. Analytics]

- [ ] All events in the instrumentation table fire in the correct sequence for a full share flow
- [ ] No events fire for unauthenticated users unless explicitly listed
- [ ] Event properties match the schema in the table above (verified in Amplitude)

---

## Success Metrics

> These are observed after launch, not acceptance gates.

| Metric | Target | Timeframe |
|--------|--------|-----------|
| [e.g. Shares per active user] | [≥ 0.5 / week] | [30 days post-launch] |

---

## Future Enhancements (Out of Scope)

- [Enhancement] — deferred because [reason]

---

## Open Questions

| Question | Owner | Status |
|----------|-------|--------|
| [e.g. Should comments be real-time?] | [PM / Design] | Unresolved |


## Related

- [Problem framing](../02_generation/user-research/problem-framing.md)
- [Opportunity assessment](../01_strategy/product-market-fit/opportunity-assessment.md)
- [INDEX](../INDEX.md)

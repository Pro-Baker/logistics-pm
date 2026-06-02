# Logistics PRD Template

This template is derived from real freight forwarding PRDs. Follow this structure when generating PRDs for logistics features.

---

## Overview
[1-2 sentences: what this feature does and why it matters. State the integration context.]

## Goals
- [Goal 1: measurable outcome]
- [Goal 2: measurable outcome]
- [Goal 3: measurable outcome]

## Non-goals
- [What this explicitly does NOT do]
- [Adjacent scope that is out of bounds for this phase]

---

## Component Sections

Break the feature into logical components. For each component:

### Component N: [Name]

[Brief description of what this component handles.]

#### Data points

| Field | Description | Source |
|-------|-------------|--------|
| [Field name] | [What it represents] | [Where it comes from] |

#### Calculated fields
- **[Field name]** = [Formula or derivation logic]

#### Key considerations
- [Edge cases, partial states, audit requirements]
- [How this component relates to other components]

---

## Integration Architecture

### Data flow
- **[System A] -> App**: [What data flows in]
- **App -> [System B]**: [What data flows out]

### Sync frequency
- [Real-time / webhook / polling interval. Justify the choice.]

### Error handling
- [What happens when sync fails. Retry logic. User notification.]
- [Reconciliation approach for data discrepancies]

---

## Open Questions
- [Unresolved decision 1]
- [Unresolved decision 2]
- [Frame as questions, not assumptions]

---

## Success Metrics
- [Product metric: adoption, time saved, user satisfaction]
- [Operational metric: sync reliability, error rate, quota utilization]
- [Business metric: revenue impact, risk reduction, cost savings]

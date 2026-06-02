---
name: eval-framework
description: "This skill evaluates the quality of AI-generated PM artifacts (PRDs, specs, user stories, analyses). It should be used when the user asks to 'evaluate this PRD', 'score this spec', 'review this output', 'is this good enough', 'check quality', or 'run an eval'. It provides a structured rubric that scores artifacts on completeness, domain accuracy, actionability, style consistency, and metric specificity. This is the quality gate that prevents shipping mediocre AI-generated product docs."
---

# Eval Framework for PM Artifacts

## Purpose

Measure whether an AI-generated PM artifact is good enough to use. Most PM plugins generate output but provide no mechanism for assessing quality. This skill closes that gap with a structured rubric.

## When to Use

- After generating a PRD, spec, or user story with this plugin
- When the user pastes an existing document and asks for a quality review
- When comparing two versions of a document (before/after, draft/final)
- Before shipping any AI-generated artifact to stakeholders

## Instructions

1. Read `references/rubric-details.md` for the full scoring criteria.
2. Score the artifact on 5 dimensions (1-5 scale each, 25 points max).
3. For each dimension, provide:
   - Score (1-5)
   - One-sentence justification
   - One specific improvement suggestion (if score < 4)
4. Calculate the total score and assign a verdict.
5. Present results in the scorecard format below.

## Scoring Dimensions

| # | Dimension | What it measures |
|---|-----------|-----------------|
| 1 | **Completeness** | Are all required sections present? Are there gaps in logic or missing components? |
| 2 | **Domain accuracy** | Is freight/logistics terminology used correctly? Are workflows described accurately? Do integration points reflect how systems actually work? |
| 3 | **Actionability** | Could an engineer start building from this? Are acceptance criteria specific enough? Are edge cases addressed? |
| 4 | **Style consistency** | Does it match the user's writing style from reference docs? Is the level of detail consistent? Is the tone appropriate? |
| 5 | **Metric specificity** | Are success metrics measurable? Are targets defined? Is there a mix of product, operational, and business metrics? |

## Scoring Scale

| Score | Label | Meaning |
|-------|-------|---------|
| 5 | Excellent | Ready to share with stakeholders as-is |
| 4 | Good | Minor polish needed, no structural issues |
| 3 | Adequate | Usable but has meaningful gaps to fill |
| 2 | Weak | Needs significant rework before sharing |
| 1 | Poor | Missing critical content or fundamentally flawed |

## Verdict Thresholds

| Total Score | Verdict | Action |
|-------------|---------|--------|
| 21-25 | **Ship it** | Ready to share with stakeholders |
| 16-20 | **Polish** | Address the low-scoring dimensions, then ship |
| 11-15 | **Rework** | Significant gaps; regenerate or rewrite weak sections |
| 5-10 | **Start over** | Fundamental issues; re-scope and regenerate |

## Output Format

Present the evaluation as:

```
# Eval: [Document Title]

| Dimension | Score | Justification | Improvement |
|-----------|-------|---------------|-------------|
| Completeness | X/5 | [reason] | [suggestion] |
| Domain accuracy | X/5 | [reason] | [suggestion] |
| Actionability | X/5 | [reason] | [suggestion] |
| Style consistency | X/5 | [reason] | [suggestion] |
| Metric specificity | X/5 | [reason] | [suggestion] |

**Total: XX/25**
**Verdict: [Ship it / Polish / Rework / Start over]**

## Key improvements needed
1. [Most impactful fix]
2. [Second most impactful fix]
```

## Notes

- Be honest. A 25/25 score should be rare. Most first drafts land in the 14-18 range.
- Domain accuracy is the hardest dimension for generic AI to score well on. Weight your feedback here.
- Style consistency can only be scored if reference docs exist in `reference-docs/`. If none exist, score as N/A and note it.

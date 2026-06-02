# logistics-pm

A domain-specific product management plugin for freight forwarding and logistics teams. Built to extend generic PM copilots with the vertical expertise they lack: freight workflows, industry terminology, logistics-tuned PRD generation, and a quality evaluation framework.

## The Problem

Generic PM copilots generate decent PRDs for SaaS features. But they fall apart on logistics:
- They don't know the difference between FCL and LCL, or when it matters
- They miss integration architecture sections (sync direction, failure handling, API quotas)
- They produce specs that an engineer in freight-tech can't build from
- They have no mechanism to evaluate whether their output is actually good

## What This Plugin Does

**4 skills** that auto-fire based on context:

| Skill | What it adds |
|-------|-------------|
| `freight-domain-knowledge` | Industry terminology, core workflows (quoting, booking, tracking, invoicing), common integrations (QuickBooks, carrier APIs, rate providers), B2B shipping stakeholder dynamics |
| `logistics-prd-generation` | PRD template tuned for logistics features. Adds component-based structure, data sync architecture, speed constraints, compliance sections. Derived from real freight forwarding PRDs |
| `eval-framework` | 5-dimension quality rubric (completeness, domain accuracy, actionability, style consistency, metric specificity). Scores output 1-25 with a ship/polish/rework/start-over verdict |
| `style-matching` | Reads your existing PRDs from `reference-docs/` and replicates your structure, tone, and level of detail. Your docs, your voice |

**2 commands** for explicit workflows:

| Command | What it does |
|---------|-------------|
| `/logistics-pm:write-spec` | End-to-end PRD generation: domain context + your template + your style + eval scorecard |
| `/logistics-pm:rfq-analysis` | Breaks down an RFQ into structured route/cargo/service tables with missing information flags |

**Reference docs** included:
- Two real freight forwarding PRDs (credit limit management, rate benchmarking) as style examples
- User story template for Linear ticket creation

## Quick Start

1. Clone this repo into your Cowork plugins directory
2. Add your own PRDs to `reference-docs/` for personalized style matching
3. Connect Linear via the included `.mcp.json` (optional)
4. Use `/logistics-pm:write-spec [feature]` to generate your first logistics PRD

## Plugin Structure

```
logistics-pm/
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json
├── README.md
├── CONNECTORS.md
├── skills/
│   ├── freight-domain-knowledge/
│   │   └── SKILL.md
│   ├── logistics-prd-generation/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── prd-template.md
│   ├── eval-framework/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── rubric-details.md
│   └── style-matching/
│       └── SKILL.md
├── commands/
│   ├── write-spec.md
│   └── rfq-analysis.md
└── reference-docs/
    ├── credit-limit-prd.md
    ├── xeneta-prd.md
    └── sample-user-story.md
```

## How It Differs from Generic PM Plugins

| Capability | Generic PM plugin | logistics-pm |
|------------|-------------------|-------------|
| Domain knowledge | None | Freight forwarding terminology, workflows, integrations |
| PRD sections | Standard template | + Integration architecture, sync design, compliance, financial risk |
| Style matching | No | Reads your reference docs and replicates your writing patterns |
| Output evaluation | No | 5-dimension rubric with scoring and verdict |
| RFQ analysis | No | Structured extraction of routes, cargo, service requirements |

## Built With

- Real PRDs from a freight forwarding B2B application
- Domain knowledge from hands-on product management in the forwarding industry
- Eval framework principles from Anthropic's documentation on developing tests for AI systems
- Prompt architecture patterns from open-source PM copilot research

## Author

Vishal Baker -- Product Manager in B2B freight forwarding, building AI product tools.

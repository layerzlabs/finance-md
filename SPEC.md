# FINANCE.md — Specification v0.1 (draft)

*May 2026 — early draft, format not yet stable*

---

## Overview

A `FINANCE.md` file is a Markdown document with a short YAML front matter block. The front matter is machine-readable by any agent or tool — it carries only the small set of facts that need to be structured. The Markdown body carries everything else (conventions, glossary expansion, rationale) in free prose.

> **Design principle.** Keep the YAML small. Conventions live in the body. Agents quote relevant lines of the body when answering — they never need to interpret a 200-line YAML.

---

## File structure

```
FINANCE.md
├── YAML front matter     ← short, machine-readable metadata
└── Markdown body         ← all conventions, in free prose
```

---

## YAML front matter

### Required

| Field | Type | Description |
|---|---|---|
| `finance_md` | string | Spec version. Current: `"0.1"` |
| `model_name` | string | Name of the model, deal, entity, or project this file governs |
| `currency` | string | Primary reporting currency, ISO 4217 (e.g. `EUR`, `USD`, `GBP`) |

### Optional

| Field | Type | Description |
|---|---|---|
| `secondary_units` | `string[]` | Non-monetary units used in the model: `tonnes`, `SKU`, `MW`, `kWh`, `tokens`, `users`, `seats`, … Free-form. |
| `language` | string | ISO 639-1 code of the model's working language (e.g. `fr`, `en`, `es`). Tells agents which language to write in by default. |
| `owners` | `string[]` | Free-form list of people responsible for these conventions — emails, names, or roles. |
| `sources` | `string[]` | Free-form list of upstream systems feeding the model — `netsuite`, `salesforce`, `manual_excel`, `bank_feeds`, `pennylane`, … |
| `glossary` | `{ [term]: definition }` | Map of company-specific or redefined terms. Agents apply these definitions in preference to generic financial ones. |
| `inherits_from` | string \| null | Path or URL to a parent `FINANCE.md` (sector or organization-wide template). |
| `model_id` | string | Tool-specific identifier (e.g. a Layerz UUID). Set automatically by tools that generate `FINANCE.md` from a model. |

That's it for the front matter. Everything else — accounting conventions (EBITDA, working capital, FX, net debt, tax), closing calendar, rationale, audit trail — belongs in the Markdown body.

---

## Markdown body

The body is **free prose**. No section is mandatory. Suggested headings, in rough order:

```markdown
## Context

What this entity does, what this model is for, who uses it.

## Closing calendar

When books close, review cadence, who validates actuals.

## Units & sign convention

If the model uses `thousands` or another denomination implicitly, state it.
If costs are positive in the P&L, state it. One worked example beats five rules.

## EBITDA

Definition (IFRS16 in/out, one-offs, SBC), with rationale.

## Working capital

DSO/DPO basis, what's in and out, target days.

## Currency & FX

Multi-currency conventions. Omit when single-currency.

## Net debt

Bridge items, minority treatment, restricted cash. Omit when not relevant.

## Tax

Rate(s), basis (statutory / effective / cash), deferred treatment.

## Glossary

Prose expansion of glossary terms that need more than one line.
```

Use only the sections that apply. A budget model probably has no Net Debt section. A SaaS FP&A model probably has no Tax section beyond a one-liner.

---

## Hierarchy and inheritance

A `FINANCE.md` can point to a parent file via `inherits_from`. The hierarchy is typically:

```
Sector       FINANCE.md  ← published reference (PE LBO, SaaS FP&A, infra…)
  └── Organization  FINANCE.md  ← group-wide
        └── Model    FINANCE.md  ← deal- or model-specific
```

Inheritance is purely declarative: a child file extends or contradicts its parent, but consumers are responsible for merging. Tools may surface a "this convention came from the parent" badge in their UI.

---

## Versioning

`FINANCE.md` files are versioned alongside the model they govern — through git when checked in, through model snapshots when stored by a modeling tool (e.g. Layerz keeps a row in `model_versions` on every save).

There is no `version`, `date`, or `changelog` field in the spec — those concerns are handled by the underlying version-control system. Keep the file short; let git/snapshots do the rest.

---

## Validation

A `FINANCE.md` is **valid** when:

- `finance_md` is a recognised spec version
- `model_name`, `currency` are present and non-empty
- `currency` is a 3-letter ISO 4217 code
- `language` (if set) is a 2-letter ISO 639-1 code
- The YAML parses
- `glossary` (if set) is a map of strings

Validators may emit warnings (not errors) for:

- A FINANCE.md over 5 000 characters (the spec is intentionally compact)
- A `glossary` with more than ~20 entries (keep the rest in the body)
- An empty body (the YAML alone rarely carries enough context)

---

## Machine consumption example

```python
import yaml

with open("FINANCE.md") as f:
    raw = f.read()

# Split front matter / body
_, fm, body = raw.split("---", 2)
data = yaml.safe_load(fm)

assert data["finance_md"] == "0.1"
print(data["model_name"], data["currency"])
print(data.get("glossary", {}).get("Marge brute"))
print(body.strip()[:200])  # first lines of the conventions prose
```

---

## Status

This is a **0.1 draft**. The format is being explored in the open; field names, defaults, and validation rules may change before a 1.0 is cut. Feedback and PRs welcome.

---

*FINANCE.md Spec v0.1 — May 2026*

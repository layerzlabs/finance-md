# FINANCE.md

**The standard that encodes financial conventions for AI agents and modeling tools.**

Like `CLAUDE.md` encodes a project's conventions for Claude, like `AGENTS.md` encodes agent capabilities — `FINANCE.md` encodes an organization's financial conventions for any agent or tool that models.

📄 [Read the standard on the web](https://layerz.cc/finance-md) · 📖 [Why it exists](https://layerz.cc/blog/finance-md-standard)

---

## The problem

Every time you start a session with an AI agent on a financial model, you repeat yourself:

> "Amounts are in thousands. Costs are positive. Books close on the 10th. We report on a management basis, not IFRS. 'Marge brute' here means revenue minus purchases only — it's not gross profit."

This context lives in your head, gets pasted into prompts, and evaporates between sessions. There is no persistent, machine-readable layer that tells agents *how this organization thinks about money*.

**FINANCE.md is that layer.**

---

## What it is

A `FINANCE.md` file is a short YAML front matter block (machine-readable) followed by a free-prose Markdown body (human-readable). It encodes:

- **Metadata** in the front matter: model name, currency, language, sources, owners, glossary — the small set of facts an agent needs at a glance.
- **What the model is for** in the body: what it produces, for whom, by when. An agent building a lender-facing budget behaves differently from one filling in a template.
- **How the statements are built**: the sections and key lines of the P&L, cash flow and balance sheet, and how they connect — net income into retained earnings, closing cash back to the cash flow. This is what stops an agent from inventing a structure nobody asked for.
- **Conventions and rationale**: units, sign, closing calendar, and any accounting policy the model actually has (EBITDA basis, net debt perimeter, working capital), *and why*.

It is not:
- A generic modeling playbook (that's your cookbook)
- A model definition (that's your MDK or schema)
- A data format (that's your API)

The format is intentionally compact — a 100-line file beats a 1 000-line YAML every time. Conventions belong in prose; the YAML carries only what is genuinely structured.

---

## Format (v0.1 — draft)

```yaml
---
finance_md: "0.1"
model_name: "Distrib SAS — FY2026 budget"
currency: EUR
secondary_units: [tonnes]
language: fr
owners: ["cfo@distrib.example"]
sources: [pennylane, manual_excel]
glossary:
  Marge brute commerciale: "Revenue minus purchase cost only. Excludes logistics."
  Tonnage: "Volume delivered, in tonnes. Capacity-planning metric, not a billing unit."
---

# Conventions

## EBITDA

Excludes IFRS16 — French GAAP entity. Operating leases stay above EBITDA as
rent expense. Sponsor convention; this is the bank-facing definition.

## Working capital

DSO on revenue (45 days target), DPO on purchases (50 days). Inventory tracked
separately in days of COGS.

…
```

Required front-matter fields: `finance_md`, `model_name`, `currency`. Everything else is optional. See [`SPEC.md`](./SPEC.md) for the full reference.

---

## Hierarchy

A `FINANCE.md` can declare a parent via `inherits_from`. The hierarchy is typically:

```
Sector       FINANCE.md  ← published reference (PE LBO, SaaS FP&A, infra…)
  └── Organization  FINANCE.md  ← group-wide
        └── Model    FINANCE.md  ← deal- or model-specific
```

Inheritance is declarative: a child file extends or contradicts its parent, but consumers are responsible for merging.

---

## Using FINANCE.md

### Claude — system prompt

Paste the file contents (front matter + body) into your system prompt:

```
You are a financial modeling assistant. The model's financial conventions
are defined below. Always apply them unless the user explicitly overrides one.

<<< FINANCE.md >>>
```

### Claude Code — CLAUDE.md

Reference it in your project's `CLAUDE.md`:

```markdown
@FINANCE.md
```

Claude Code picks the conventions up at session start.

### Cursor — project rules

Place `FINANCE.md` at the root of your financial-modeling project. Cursor auto-injects project-level files. Add an explicit reference in `.cursor/rules`:

```
Always read and apply FINANCE.md before any financial modeling task.
```

### MCP servers

Any MCP server can expose a `read_conventions` tool that returns the FINANCE.md for a given model. Layerz, for example, ships three tools (`layerz_get_finance_md`, `layerz_set_finance_md`, `layerz_generate_finance_md`) that let an agent push its local `FINANCE.md` into a Layerz model at session start, then operate under those conventions.

---

## Placement

- **Organization-level**: root of a financial-modeling repository (e.g. `models/FINANCE.md`)
- **Model-level**: alongside a specific model (e.g. `models/ma/deal-x/FINANCE.md`)

> **Note**: `FINANCE.md` belongs in a financial-modeling project, not at the root of a generic company repository where the filename could be confused with expense policies or HR finance docs.

---

## Examples

| Use case | File |
|---|---|
| SME — monthly budget | [`examples/sme-budget/FINANCE.md`](./examples/sme-budget/FINANCE.md) |
| LBO / M&A | [`examples/lbo/FINANCE.md`](./examples/lbo/FINANCE.md) |
| SaaS FP&A | [`examples/saas-fpa/FINANCE.md`](./examples/saas-fpa/FINANCE.md) |
| Infrastructure / Concession | [`examples/infra/FINANCE.md`](./examples/infra/FINANCE.md) |

Start from [`TEMPLATE.md`](./TEMPLATE.md) for a blank scaffold.

---

## Status

This repository is a **0.1 draft**. The format is being explored in the open: field names, defaults, and validation rules may change before a 1.0 is cut. Treat the current schema as a working proposal, not a stable contract.

---

## Roadmap

- [x] Initial draft (v0.1, this repo)
- [ ] Schema 1.0 stable
- [ ] MCP reference implementations
- [ ] Validator CLI (`npx finance-md validate`)
- [ ] Convention linter (validate agent outputs against FINANCE.md)
- [ ] Translations / locale-specific conventions

---

## Where this fits

`FINANCE.md` is one of a small family of open entry points to [Layerz](https://app.layerz.cc):

| Project | Role |
|---------|------|
| **`finance-md`** (you are here) | The **standard**: how an organization encodes its financial conventions for any agent |
| [`cookbook`](https://github.com/layerzlabs/cookbook) | The **recipes**: prompts and patterns for doing financial work with AI agents |
| [Layerz MCP](https://layerz.cc/for-agents) | The **tool**: how an agent drives Layerz to build structured, versioned models |
| [`slides-for-claude`](https://github.com/layerzlabs/slides-for-claude) | The **presentations**: turn a model or a topic into a self-contained HTML deck |

The standard tells an agent *what your numbers mean*. The tool gives it *a place to build that does not drift*. The cookbook shows *what to ask for in the first place*.

---

## Contributing

This is an open standard. Contributions welcome:

- Additional examples for common deal types
- Schema extensions
- Tool integrations and use-case guides

Open a PR or a discussion.

---

## License

MIT — see [`LICENSE`](./LICENSE).

---

*Initiated by [Layerz](https://layerz.cc)*

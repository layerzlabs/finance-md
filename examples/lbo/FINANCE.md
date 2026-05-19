---
finance_md: "0.1"
model_name: "Project Granite — LBO model"
currency: EUR
language: en
owners: ["lead@granite-pe.example", "associate@granite-pe.example"]
sources: [data_room, manual_excel, target_audit_2025]
glossary:
  Management EBITDA: "Reported EBITDA before any restatement, as per management accounts."
  Adjusted EBITDA: "Management EBITDA plus run-rate synergies (year-1 only), minus normalised one-offs above 1% of revenue. The covenant basis."
  Net debt (covenant): "Total financial debt + IFRS16 lease liabilities + earn-outs − unrestricted cash. Restricted cash and minimum operating cash (€2M) excluded."
  Leverage: "Net debt (covenant) / Adjusted EBITDA (LTM)."
---

# Conventions

## Context

PE-backed acquisition (mid-market, industrial). Consolidated group level,
SPV + OpCo. IFRS reporting required by lenders. Budget rate for the P&L is
locked at signing. Single currency (EUR) — pan-European target with marginal
exposure to GBP and PLN, hedged via 12m forwards.

## Units & sign convention

All amounts in **millions EUR**. Costs are **positive** in the P&L.

## EBITDA

Two flavours, always reported side by side:

- **Management EBITDA** — as reported, no adjustments. Baseline for QoE and
  bridge to Adjusted EBITDA.
- **Adjusted EBITDA** — the covenant basis. Year-1 only: includes the
  €1.8M of identified procurement synergies (run-rate, not phased). Throughout:
  excludes one-offs above 1% of revenue with explicit rationale.

**Includes IFRS16** lease costs as operating expense (kept above EBITDA).
Lease liabilities reappear in net debt — see below. Sponsor convention.

**Stock-based compensation**: excluded from Adjusted EBITDA (treated as a
financing item via the MIP, accrued separately).

## Working capital

Standard NWC: trade receivables + inventories + prepayments − trade payables −
deferred income. DSO on **billings**, DPO on **COGS**. Targets from
management: DSO 55, DPO 65, DIO 70.

Excluded from NWC: cash, financial debt, deferred tax, restructuring accruals.

## Net debt

Bridge to **net debt (covenant)**:

- Senior debt (TLA + RCF drawn)
- Unitranche
- IFRS16 lease liabilities (all)
- Earn-outs (at expected value)
- Minus: cash and equivalents
- Minus: minimum operating cash buffer (€2M, deducted only for ratio purposes)
- Minus: restricted cash (escrow, blocked deposits)

Minority interests are **excluded** from net debt (PIK note to minority is
treated as quasi-equity at closing).

## Currency & FX

Reporting in EUR at budget rate (€1 = $1.08, locked Q4 2025). P&L items at
budget rate. Balance-sheet items at closing rate. FX variance reported as a
separate line below operating EBIT, not within operating items.

## Tax

Statutory rates by jurisdiction: FR 25.83%, DE 30%, NL 25.8%, PL 19%.
Effective rate model overlay: assume 28% blended (pre-financing structure)
for the operating model; financing tax shield modelled separately on debt
service.

Deferred tax modelled at the SPV level (intangible amortisation tax shield).

## Glossary expansion

**Management vs. Adjusted EBITDA** is the single biggest source of bridge
errors in deal models. Agents working on this model must always quote which
flavour they refer to. The bridge from Management to Adjusted EBITDA is in the
QoE schedule (separate model).

**Restricted cash** at closing: €3.4M (Polish subsidiary escrow). Not available
for debt service — excluded from the leverage ratio.

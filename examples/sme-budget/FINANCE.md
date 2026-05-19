---
finance_md: "0.1"
model_name: "Distrib SAS — FY2026 budget"
currency: EUR
secondary_units: [tonnes]
language: fr
owners: ["cfo@distrib.example"]
sources: [pennylane, manual_excel]
glossary:
  Marge brute commerciale: "Revenue minus purchase cost only. Excludes logistics, packing and handling."
  EBITDA management: "EBITDA before one-offs above 2% of revenue. Excludes restructuring and earn-outs."
  Tonnage: "Physical volume delivered, in tonnes. Tracked for capacity planning only — not a billing unit."
---

# Conventions

## Context

Regional food distributor (B2B). 12 warehouses in Île-de-France. ~€80M revenue,
monthly budget refreshed quarterly, presented to the bank under covenants.

This file governs the FY2026 budget. Restatements vs. prior years are tracked
in the model's `actuals` Layer, not here.

## Units & sign convention

All amounts in **thousands EUR**. Costs are **positive** in the P&L
(net income = revenue − costs). Tonnage is in **tonnes** (kt = thousands of tonnes).

## Closing calendar

Books close on the 10th of the following month (Pennylane export). Management
review on the 20th. Budget variance reported to the bank within 30 days of close.

## EBITDA

**Excludes IFRS16** — French GAAP entity, operating leases stay above EBITDA as
rent expense. Lease commitments are documented in the off-balance-sheet section
of the annual statement and are *not* added to net debt in this model.

**Excludes one-offs above 2% of revenue.** Below that threshold, items stay in
"recurring" — agents must not silently normalise items below the threshold.
Above it, the item moves to a dedicated "Non-recurring" section with a one-line
rationale.

Stock-based compensation: not applicable (private SME, no SBC plan).

## Working capital

DSO measured on **revenue** (not billings — invoicing is concurrent with delivery).
Target DSO: 45 days. DPO measured on **purchases** (not COGS). Target DPO: 50 days.
Inventory turnover monitored separately in days of cost-of-goods.

Excluded from WC: cash, short-term debt, accruals for restructuring (one-off).

## Tax

Statutory IS rate: 25%. CVAE: estimated at 0.5% of value added.
Deferred tax not modelled (private SME, no IFRS reporting).

## Glossary

- **Marge brute commerciale** is the bank-facing margin metric. It is *not*
  gross profit in the IFRS sense — logistics and handling are below it, in
  operating expenses. Quoted in covenants as "GM commerciale ≥ 18%".

- **Tonnage** is monitored to validate the capacity assumption (~120 kt / year
  per fully utilised warehouse). It does not enter the P&L directly.

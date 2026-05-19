---
finance_md: "0.1"
model_name: "Concession Aurora — Toll road operator"
currency: EUR
secondary_units: [vehicles, km]
language: en
owners: ["finance@aurora-infra.example"]
sources: [erp_sap, manual_excel, traffic_management_system]
glossary:
  DSCR: "Debt Service Coverage Ratio: CFADS / (interest + principal) for the period. Lender covenant."
  CFADS: "Cash Flow Available for Debt Service: operating cash flow after maintenance capex and tax, before interest and principal."
  DSRA: "Debt Service Reserve Account. Restricted cash equal to next 6 months of debt service. Excluded from net debt."
  RAB: "Regulated Asset Base. Net book value of regulated assets, indexed by RPI annually."
  Maintenance capex: "Routine and major maintenance to preserve the asset. Above EBITDA. Distinct from expansion capex (below EBITDA)."
  Concession term: "Remaining contractual period to grant expiry. 18.4 years at FY2026 start."
---

# Conventions

## Context

Toll road concession (motorway operator). Concession term: 35 years total,
18.4 remaining at FY2026 start. Long-term project finance model, with senior
debt and mezzanine layers, RPI-indexed revenue, and a regulated maintenance
schedule. IFRS reporting.

## Units & sign convention

All amounts in **millions EUR**. Costs are **positive** in the P&L. Traffic
volumes in **vehicles** (PCUs — Passenger Car Units) and **kilometres**.

## EBITDA

**Includes IFRS16** — operational leases are immaterial.

**Maintenance capex stays above EBITDA** as the asset wears out continuously
and the maintenance schedule is contractual. This is an infra-specific
convention: routine maintenance is treated as operating cost, not capex.
**Major periodic maintenance** (resurfacing, structural works) is also above
EBITDA, capitalised over its useful life, with the amortisation flowing
through EBITDA via the maintenance schedule.

**Expansion capex** (additional lanes, new interchanges) is below EBITDA —
this is true growth capital and a regulatory event.

## Revenue & indexation

Toll revenue: indexed annually on the RPI cap (max 70% of national CPI per
the concession contract). Traffic forecasts: from the central case of the
2024 traffic study, with sensitivity scenarios at ±15%.

Other revenue: service area concessions (fixed annual fees + variable on
turnover), parking, advertising. Modeled separately, treated as recurring.

## Working capital

Minimal in concessions. DSO ~30 days (toll receipts are mostly real-time via
electronic systems). DPO ~60 days (maintenance contractors). No inventory.

## Net debt and reserve accounts

Net debt = senior debt + mezzanine + earn-outs − **unrestricted cash only**.

**Restricted cash explicitly excluded** from net debt:
- DSRA (next 6 months of debt service)
- Major maintenance reserve (next 24 months of contractual maintenance)
- Concession-end fund (reimbursement to grantor at hand-back)

The leverage covenant uses **gross debt / EBITDA**, not net — restricted cash
is not netted off in the lender view.

## Covenants

Two binding ratios:
- **DSCR ≥ 1.20×** (locked-in lender covenant, tested semi-annually).
- **Gross leverage ≤ 7.5×** (more theoretical — concession project finance
  ratios run higher than corporate norms).

Distribution lock-up if DSCR < 1.30× for two consecutive periods.

## Tax

Statutory IS rate 25.83%. Deferred tax modelled at the concession SPV level
(intangible amortisation of the concession right). Cash tax differs
materially from accounting tax in early years (amortisation tax shield).

## Glossary expansion

**RAB** does not apply to a road concession in the strict regulatory sense.
We use it informally to refer to the depreciated value of the maintenance-
preserved asset base, for internal capital-allocation discussions only. It
must not be quoted to regulators or lenders.

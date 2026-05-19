---
finance_md: "0.1"
model_name: "SaaS Co — FY2026 FP&A"
currency: USD
secondary_units: [seats, accounts]
language: en
owners: ["vp-finance@saasco.example"]
sources: [netsuite, salesforce, manual_excel]
glossary:
  ARR: "Annualised Recurring Revenue. Committed contracted revenue × 12. Excludes professional services and usage-based revenue."
  NRR: "Net Revenue Retention: (ARR_start + expansion − churn − contraction) / ARR_start. Trailing 12 months."
  CAC: "Customer Acquisition Cost: S&M spend (direct only, no brand) / new logos in the period."
  CAC payback: "CAC / (ARR per new customer × gross margin). Target < 18 months."
  LTV: "(ARPU × gross margin) / churn rate. Reported at cohort level only."
---

# Conventions

## Context

B2B SaaS, mid-market HR software. 350 customers, ACV $28k.
US HoldCo + France OpCo. Internal management reporting in USD;
local statutory accounts kept under US GAAP (HoldCo) and French GAAP (OpCo).
This file governs the FP&A monthly close.

## Units & sign convention

All amounts in **thousands USD**. Costs are **positive** in the P&L.

## Closing calendar

Books close on day 7 of the following month. Salesforce ARR snapshot taken
the same day (frozen for the close). Management review on day 12.

## EBITDA

**Includes IFRS16** — the office lease is the only material lease, small
relative to revenue. This contradicts the PE/LBO convention; agents must not
assume IFRS16 exclusion.

**Excludes stock-based compensation** from management EBITDA (tracked
separately in the equity dilution schedule). When reporting to investors,
SBC-adjusted EBITDA is used.

**Excludes one-offs above 0.5% of ARR** — more conservative than the typical
1% revenue threshold. Investment in S&M is *not* a one-off, ever.

## Revenue recognition

IFRS15. Annual contracts recognised ratably (1/12 per month). Multi-year:
same, no upfront acceleration. Usage-based add-ons recognised as consumed.
Implementation fees: deferred unless distinct from the subscription.

## Working capital

DSO measured on **billings** (not revenue). SaaS-specific: subscription
revenue is ratable but cash is collected annually — billings is the right
basis. Deferred revenue is a liability (negative WC) but excluded from
operational WC measures because it unwinds on a fixed schedule.

Included in WC: trade receivables, prepayments.
Excluded: cash, deferred revenue, short-term debt.

## Currency & FX

Budget rate locked in December for the next FY. P&L at budget rate; FX
variance reported as a single line below operating EBIT. Balance sheet at
closing rate (IFRS standard).

OpCo (France) reports monthly in EUR, translated to USD at budget rate for
consolidation. EUR is the only secondary currency — no other entities.

## Tax

Cash basis for FCF projections (cash conversion drives SaaS valuation).
Country rates: US 21%, FR 25.72%. Deferred tax excluded from the FCF bridge.

## Glossary expansion

**ARR** is the headline KPI in every board pack. Definition is strict:
committed contracted recurring revenue × 12. Professional services and
usage-based add-ons are *not* in ARR even when invoiced concurrently.

**LTV** is meaningful only at the cohort level. The "blended LTV" sometimes
quoted in pitches has no basis here and is not produced from this model.

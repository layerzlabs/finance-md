---
finance_md: "0.1"
model_name: "[Model or deal name]"
currency: EUR
# secondary_units: [tonnes, SKU]    # optional, free-form
# language: fr                      # optional, ISO 639-1
# owners: ["finance@example.com"]   # optional, free-form list
# sources: [netsuite, manual_excel] # optional, free-form list
# glossary:                         # optional, term → one-line definition
#   Marge brute commerciale: "Revenue minus purchase cost only (excludes logistics)"
# inherits_from: null               # optional, URL/path to a parent FINANCE.md
---

# Conventions

## Context

[What does this entity do? What is this model for? Who uses it, and by when?]

## Statement structure

[The sections and key line items of each statement, and how they connect.
Replace the example below with yours. Delete the statements the model does not have.]

  P&L          [Revenue driver → gross margin → opex → EBITDA]
  Cash flow    [EBITDA → working capital → capex → net cash]
  Balance      [Net income feeds retained earnings.
                Closing cash ties back to the cash flow statement.]

## Units & sign convention

[All amounts in thousands EUR. Costs are positive in the P&L. State your convention
in one short paragraph with a worked example if there is any ambiguity.]

## Closing calendar

[For recurring models: when do books close, who validates, what's the cadence.
Omit for one-off / deal models.]

<!-- Everything below is an accounting policy. Keep a section only if this model
     actually has that policy. Delete the rest — an empty heading reads as a
     deliberate convention. -->

## EBITDA

[Definition: IFRS16 in or out, one-off threshold, SBC treatment, and *why*.]

## Working capital

[DSO/DPO basis, inclusions/exclusions, target days. Omit if not relevant.]

## Currency & FX

[Single-currency? Drop this section. Multi-currency? State the rate convention
(closing / average / budget rate) for BS and P&L.]

## Net debt

[Bridge items, minority treatment, restricted cash policy. M&A / PE models only.]

## Tax

[Statutory vs. effective vs. cash basis. Country rates if multi-jurisdiction.]

## Glossary

[Prose expansion of any glossary term that needs more than one line.]

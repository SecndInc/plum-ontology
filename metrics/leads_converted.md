---
name: leads_converted
version: 1
status: proposed
kind: base
owner: revops
description: Number of leads converted (to an account, contact and usually an opportunity), by conversion date.
source: {type: sf_report, ref: 00OKc0000013SqXMAU}
confidence: medium
last_verified: 2026-09-29
grain: lead
source_table: Lead
measure: {agg: count, column: Id}
base_filters:
  - {field: IsConverted, op: "=", value: true}
time_column: ConvertedDate
time_semantics: fiscal
dimensions:
  - {key: lead_source, column: LeadSource}
  - {key: lead_owner_title, column: Owner.Title}
filters:
  - {key: lead_source, column: LeadSource, type: picklist, allowed_values: [Referral - Team, Referral - Partner, Website, Other, Trade Show, Employee Referral, Advertisement]}
coverage_checks:
  - {name: no_opportunity, sql_predicate: ConvertedOpportunityId IS NULL, description: Converted without creating an opportunity}
  - {name: no_account, sql_predicate: ConvertedAccountId IS NULL, description: Converted lead with no converted account id}
  - {name: no_lead_source, sql_predicate: LeadSource IS NULL, description: Converted lead with no source}
  - {name: test_lead, sql_predicate: "Company IN ('Test', 'Test Company', 'vtg test')", description: Test records converted}
reconcile: {sf_report_id: 00OKc0000013SqXMAU, compare_column: RowCount, tolerance: 0}
topic: leads
format: number
aliases: ["converted leads", "lead conversions", "leads converted", "qualified leads"]
---

Counts leads with IsConverted = true by ConvertedDate (a date field, no time zone shift), as the Leads Converted by FQ / Current FQ / All Time reports do (their record count is converted leads).

In this org Status = 'Qualified' is exactly the converted set (46 of 46), so "qualified leads" and "converted leads" are the same count.

Caveats:
- Leads were mostly created and converted on the same day as a data-entry path to create an engagement (Master Opportunity); a conversion is not a marketing hand-off.
- Some conversions created no opportunity, and a few are test records (see coverage checks).
- Do not sum the converted opportunities' Amount as revenue: they are mostly Master engagement estimates, largely lost (see [[lead-converted-opportunity-amount]]).

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 23

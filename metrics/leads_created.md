---
name: leads_created
version: 1
status: proposed
kind: base
owner: revops
description: Number of leads created, by lead created date.
source: {type: sf_report, ref: 00OKc0000013SqYMAU}
confidence: medium
last_verified: 2026-09-29
grain: lead
source_table: Lead
measure: {agg: count, column: Id}
base_filters: []
time_column: CreatedDate
time_semantics: fiscal
dimensions:
  - {key: lead_source, column: LeadSource}
  - {key: lead_status, column: Status}
  - {key: lead_owner_title, column: Owner.Title}
filters:
  - {key: lead_source, column: LeadSource, type: picklist, allowed_values: [Referral - Team, Referral - Partner, Website, Other, Trade Show, Employee Referral, Advertisement]}
  - {key: lead_status, column: Status, type: picklist, allowed_values: [New Lead, New, Working, Nurturing, Internal Debrief, Qualified]}
coverage_checks:
  - {name: no_lead_source, sql_predicate: LeadSource IS NULL, description: Lead with no source; shows as blank in by-source breakdowns}
  - {name: test_lead, sql_predicate: "Company IN ('Test', 'Test Company', 'vtg test')", description: Test records counted as leads}
  - {name: sept_2026_list_import, sql_predicate: "Status = 'New Lead'", description: "Status 'New Lead' is used only by the 2026-09-01 bulk list import of 100 prospects"}
reconcile: {sf_report_id: 00OKc0000013SqYMAU, compare_column: RowCount, tolerance: 0}
topic: leads
format: number
aliases: ["new leads", "leads created", "lead volume", "# of leads"]
---

Counts every lead record by CreatedDate (fiscal year = calendar year, org time zone America/New_York), with no status or source filter, the same way the org's lead reports count (Leads Created Current FQ, Sample Report: # of Leads, Marketing Exec Leads by Source).

Caveats:
- 100 of the 143 leads created in 2026 Q3 come from one list import at 2026-09-01 21:32 UTC (all Referral - Team, USD, 96 still 'New Lead'). Any 2026 trend is dominated by it; see [[lead-bulk-import-2026-09]].
- 6 leads were seeded at org creation (2025-01-20) and 6 have test company names; they are included, as the reports include them.
- Before September 2026 leads were mostly created only to be converted on the same day, so lead volume is not a measure of marketing demand.


## Reviewer note
The coverage check sept_2026_list_import uses Status = 'New Lead', which flags only the 96 unconverted import leads. It misses the 4 import leads already converted (now 'Qualified'), and any further lead that moves out of 'New Lead' will silently drop out. Use CreatedDate = TIMESTAMP '2026-09-01 21:32:44 UTC' (or CreatedById plus that timestamp) so the check covers all 100. The caveat 'mostly created only to be converted on the same day' needs the same pre-import qualification noted on c70.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 29

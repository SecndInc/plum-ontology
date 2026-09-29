---
name: push_revenue
version: 1
status: proposed
kind: base
owner: revops
description: PUSH's own net revenue on won projects (Sales Opportunities), i.e. media fees on Media work and amount minus vendor cost on Creative and Agency work, in CAD.
source: {type: sf_report, ref: 00OJQ00000NjbSo2AJ}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: sum, column: PUSH_Revenue__c}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Sales_Opportunity}
  - {field: IsWon, op: "=", value: true}
time_column: CloseDate
time_semantics: fiscal
currency: {column: PUSH_Revenue__c, convert: true}
dimensions:
  - {key: service_line, column: Type}
  - {key: operating_entity, column: Operating_Entity__c}
  - {key: client, column: Account.Name}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: media_fee_missing, sql_predicate: "Type = 'Media' AND Media_Fee__c IS NULL", description: Media project with no Media Fee %; PUSH revenue computes to 0}
  - {name: media_spend_missing, sql_predicate: "Type = 'Media' AND Total_Media_Spend__c = 0", description: Media project with no monthly media spend entered; PUSH revenue computes to 0}
  - {name: push_revenue_zero, sql_predicate: PUSH_Revenue__c = 0, description: Won project contributing zero net revenue}
topic: revenue
format: currency
aliases: ["push revenue", "net revenue", "agency revenue", "fee revenue", "margin dollars"]
---

**Definition.** The sum of `PUSH_Revenue__c` on Sales Opportunities (projects) where `IsWon = true`, dated by CloseDate on the fiscal calendar (January start), converted to CAD (corporate currency; USD rate 0.737 per CAD).
`PUSH_Revenue__c` is a formula: for Media it is `Total_Media_Spend__c × Media_Fee__c`, for everything else it is `Amount − Vendor_Cost__c`, with blanks treated as 0.

**Why IsWon rather than the report's stage list.** The PUSH Revenue - Total report (00OJQ00000NjbSo2AJ) filters StageName to Financial Setup, Kick-off, Project In Progress and Project Completion. Those stages were retired in 2026 and replaced by Closed Won. For FY2025 both give the same set of 107 projects, 1,707,070.92 CAD. For FY2026 the report's stage list catches 1 of 21 won projects and shows 0 PUSH revenue. This definition matches `gross_revenue`, which also uses IsWon. There is no reconcile, because the report runs on THIS_FISCAL_YEAR, where the stage filter is known to undercount.

**Caveats.**
- Understated for Media: 34 of 67 won CAD Media projects and all 7 USD Media projects have PUSH revenue of 0, because Media Fee % is blank or monthly media spend is not filled in. See the coverage checks.
- Never sum Master Opportunities. They carry their own engagement estimates and would double count.
- Operating entity is blank on every project before FY2026.


## Reviewer note
The coverage checks miss the biggest gap. For FY2025, media_fee_missing and media_spend_missing both flag 28 records, and push_revenue_zero flags 31. The other 3 are Media projects with a fee % and 3,401,272.08 of media spend (3.48M Amount) whose PUSH revenue is still 0, presumably a 0% fee. Only the generic zero check catches them. Add a check for Type='Media' AND Media_Fee__c IS NOT NULL AND Total_Media_Spend__c > 0 AND PUSH_Revenue__c = 0. Fix the Media caveat, which blames only a blank fee or missing spend. Also note two things: the 0.737 USD conversion is one static rate with no dated rates, and the operating_entity dimension has 1 blank FY2026 win (348,893 CAD).

## Sweep
Drafted by the revenue investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 1707070.92

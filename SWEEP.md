# Sweep sweep-20260929T2239

Snapshot 20260929T163700Z (extracted 2026-09-29T16:37:00.079Z) · model claude-opus-5-5 · 2026-09-29.

Investigate, don't paraphrase: every claim cites queries whose results contain its numbers; every metric compiled and ran on the snapshot; a second model reviewed each topic; cited queries were rerun before emitting.

## What this adds

- 34 proposed metrics: `accounts_with_activity`, `campaign_revenue_budget`, `campaign_won_value`, `clients_won`, `engagements_by_close_date`, `gross_revenue_pipeline`, `lead_conversion_rate`, `leads_converted`, `leads_converted_of_created`, `leads_created`, `lost_count`, `meetings_held`, `new_business_closed_count`, `new_business_win_rate`, `new_business_won_count`, `open_engagements`, `open_pipeline_amount`, `open_pipeline_amount_p10`, `open_pipeline_amount_p25`, `open_pipeline_amount_p50`, `open_pipeline_amount_p75`, `open_pipeline_amount_p90`, `open_pipeline_count`, `opportunities_with_activity`, `project_pipeline_amount`, `push_revenue`, `push_revenue_margin`, `pushed_open_engagements`, `revenue_budget`, `revenue_budget_attainment`, `tasks_by_due_date`, `tasks_completed`, `total_activities`, `weighted_pipeline_amount`
- 48 claims in findings/, 9 glossary terms, 18 gotchas, 11 open questions
- 24 object profiles in objects/, 188 decoded reports in reports/

## By topic

- **revenue**: 29 turns. I drafted four revenue metrics that pass the compile check. They agree with the accepted `gross_revenue`, but two things undercut them: the org's own revenue reports now undercount FY2026, and Media net revenue is understated.

**How revenue counts:**
- **Which records:** money is summed on won projects (Sales Opportunity record type, IsWon = true), dated by CloseDate on a fiscal year that starts in January, and converted to CAD at the one static rate the org has (CAD = USD / 0.737).
- **Engagements are separate:** Master Opportunities (engagements) carry their own, different Amounts. Adding them to projects double counts (c92).
- **Won stages changed in 2026:** the old won stages (Financial Setup, Kick-off, Project In Progress, Project Completion) are retired, and wins since 2026-07 go to Closed Won (c101).
- **Reports undercount FY2026:** the Gross Revenue and PUSH Revenue reports still filter on the old stages. For FY2025 they match IsWon exactly: 107 projects, 13,226,393.10 CAD gross and 1,707,070.92 CAD PUSH revenue. For FY2026 they catch 1 of 21 won projects: 348,893.2 CAD gross and 0 PUSH revenue, against 1,799,873 gross and 894,924 PUSH revenue by IsWon (c91).
- **PUSH revenue is 0 on many Media projects:** it comes out 0 on 34 of 67 won CAD Media projects and all 7 USD ones, because the fee % or monthly media spend was never entered (c102).
- **Operating entity only works from FY2026:** it is blank on every project before FY2026, and most FY2025 wins were entered after their close date (c105).

**Budget and plans:**
- **The real budget:** it sits in Campaigns of type Sales: a "2025" root with ExpectedRevenue 20,016,974.49, which equals the sum of its 18 client × service-line leaves. A middle "New Business" node repeats its children's 4,083,759, so summing every child campaign double counts (c103).
- **Campaign won rollup:** only engagements are tagged to budget campaigns, so the campaign's won-amount rollup is engagement value and includes FY2026 wins (c104).
- **Not usable as targets:** the monthly revenue plan object and the forecasting quotas are test and template data (c110).
- **Only a 2025 budget exists.**

**Metrics drafted (FY2025 results):**
- `push_revenue`: net revenue on won projects, 1,707,070.92 CAD. It uses IsWon rather than the report's stage list, and flags Media projects with no fee % or no spend.
- `push_revenue_margin`: push_revenue / gross_revenue, 12.9%.
- `gross_revenue_pipeline`: Amount on open projects, matching the Forecast Amount report. For past years it only contains projects left open with an old close date (42,000 in FY2025).
- `revenue_budget`: the root budget campaign's ExpectedRevenue, 20,016,974.49.

None of these reconcile against a report, because the reports run on the current fiscal year, where the stage filter undercounts. There is no weighted forecast metric, because Amount × Probability can't be expressed as a measure.

**Notes added:** gotchas on the retired stages, PUSH revenue being 0 on Media, the "Special Project" type no longer existing, and USD/static rate/dating; glossary entries for PUSH Revenue and the Revenue Budget.

One correction to the USD note: it says adding native amounts "overstates" the CAD total. It actually understates it, because 1 USD ≈ 1.357 CAD. Notes can't be edited, so this needs fixing in review.

**Still open:**
- **Which amount to compare to the budget:** won engagements give about 100% for FY2025 (19,948,445.47 CAD), won projects about 66% (13,226,393.10). I assumed projects and drafted no attainment metric until someone confirms.
- **Special Projects:** I assumed the budget's "Special Projects" lines correspond to the Agency type.
- **Fix at the source:** the PUSH KPI reports' stage filters should include Closed Won.
- **Data entry:** Media fee % and monthly media spend need filling in on won Media projects.
- **pipeline**: 35 turns. I defined open pipeline at the engagement level (Master Opportunities not yet won or lost), gave project pipeline its own metric, and built a weighted pipeline. The weighted one needs a workaround and will break if reps start using new probability values.

**What I established:**
- **Only two record types hold data:** Master_Opportunity (engagements) and Sales_Opportunity (projects). The Stratis record type has no records.
- **Adding the two record types double counts (c94).** 39 of the 46 open projects belong to an open engagement. The engagement's Amount is its own estimate, not a total of its projects: 12,165,496 on the engagements versus 6,884,901 on their projects.
- **Forecast category and probability (c95):** forecast category always follows the stage on open engagements (Discovery and Creds Presentation = Pipeline, Proposal = Best Case, Contract = Commit). Probability doesn't always follow: 8 open Proposals have probabilities other than the 50% default, and projects differ more.
- **Open engagement pipeline closing in FY2026, in CAD (c96):**

| Category | Deals | Amount | Weighted |
|---|---|---|---|
| Best Case | 18 | 27,947,360 | 12,658,680 |
| Commit | 23 | 15,595,996 | 14,036,396 |
| Pipeline | 6 | 100,000 | 10,000 |

- **One deal dominates (c108):** a single engagement holds 15,000,000 of the 38,273,196 FY2026 open total (native currency).
- **Close-date slippage (c111):** the Push Count field matches the pushes rebuilt from history, so it can be trusted. Most pushes happened in batches in September 2026; on 2026-09-21 alone, 12 open engagements moved from 2026 to 2027.
- **Stages rarely go backwards (c109):** 7 backward moves on 3 engagements and 3 on 3 projects. Moves between the delivery stages (e.g. Project In Progress to Project Completion) are delivery updates, not sales progress.
- **Most records entered already closed (c112):** 60 engagements and more than 120 projects first appear in history at a closed stage, and 42 engagements first appear at Contract or Proposal. Any stage-conversion or sales-cycle measure has to exclude these.
- **The sales process changed on 2026-06-08 (c113):** Creds Presentation was added, and the old won stages (Kick-off, Project In Progress, Project Completion) were switched off in favour of Closed Won. The KPI reports still filter on those old names. As a result they drop the 8 open Creds Presentation engagements and nearly all FY2026 wins.
- **Salesforce's built-in forecasting and quota records aren't usable (c114):** they cover only a handful of opportunities.

**Metrics drafted (all proposed; each compiled and ran for FY2025):**
- `open_pipeline_amount` and `open_pipeline_count`: open engagements, in CAD, by close date. Checks flag missing amounts, 0% deals, overdue close dates and probabilities the weighted metric doesn't cover.
- `project_pipeline_amount`: open projects. It matches the "Gross Revenue - Forecast Amount" report and is set to reconcile against it.
- `weighted_pipeline_amount`: amount × probability. The metric format can't multiply two fields per record, so I built it from five helper metrics, one for each probability in use (10/25/50/75/90%; 0% adds nothing). If a new probability appears, those deals drop out of the weighted total until someone adds a helper. The check on `open_pipeline_amount` flags this.
- `pushed_open_engagements`: open engagements whose close date has been pushed to a later month at least once.

**Notes added:** a glossary entry for stages and forecast categories, and warnings about double counting, outdated report stage names, history that starts mid-way, and the forecasting records.

**Questions for a reviewer, with the default I used:**
1. Does "pipeline" mean engagements or projects? Default: engagements.
2. Weight by each deal's probability or by the stage default? Default: the deal's probability, as Salesforce does.
3. Do overdue open deals stay in pipeline? Default: keep them and flag them. The overdue check uses the snapshot date (2026-09-29), so it needs moving forward with each new snapshot.

**Not covered:** stage-conversion and time-in-stage metrics (history is too incomplete for now), and pipeline against plan (the monthly revenue plan object wasn't investigated).
- **bd**: 25 turns. Business-development topic, snapshot 20260929T163700Z (15 queries used).

Established:
- Engagements are Master_Opportunity records (162); projects are Sales_Opportunity records. 165 projects link to 46 engagements, 26 projects have no parent, and 38 won engagements have no projects at all. An engagement's Amount is not the sum of its projects (c97).
- "Won" means IsWon: stage Closed Won plus Kick-off, Project In Progress and Project Completion. The BD won-count KPI reports leave out Closed Won. For FY2025 that is 41 vs 42 wins; for FY2026 it is 0 vs 20, because every FY2026 win is Closed Won (c106).
- Win rate is inflated by wins that were loaded already won. FY2025 engagements that entered the pipeline open went 3 won / 8 lost; FY2026 went 5 / 5 (c98).
- Existing-client engagements won 39 of 41 in FY2025; new business (New and New - RFP) won 3 of 11 (c87).
- Engagement Amount is dominated by large lost RFP bids. One lost bid is 60.3% of FY2026 decided engagement value, so win rate is counted by records, not money (c88).
- Operating entity is only filled from FY2026 (c89).
- FY2025 wins came from 9 clients, one of which had 13 of the 42 wins (c90).
- Business type does not always match the account's win history (c99). The 2026-07-08 bulk load was checked, and no duplicate engagements were found (c100).

Drafted (all passed):
- engagements_by_close_date: 53 in FY2025. It reproduces the "BD - # of Opportunities past FY" report (00OJQ00000NllSr2AJ) with the same filters, with a reconcile check set at zero tolerance.
- lost_count: 10.
- new_business_won_count: 3.
- new_business_closed_count: 11.
- new_business_win_rate: 27.3%.
- clients_won: 9.
- open_engagements: 1 stale open engagement dated FY2025. The current pipeline is 47 dated FY2026 and 33 dated FY2027.

Notes: glossary entries for engagement vs project, won/lost/decided, and business type/service line/operating entity. Gotchas for the stage-list won reports, the inflated win rate, and engagement Amount.

Still open:
- Is Organic Growth new or existing business? Default used: existing.
- Should win rate leave out engagements entered already won? Default used: no, keep the accepted definition.
- Bias from wins entered already won and from existing clients stays a caveat on the accepted win_rate. Operating-entity splits before FY2026 are not meaningful.
- **leads**: 30 turns. I used 17 of the 35 queries. The main finding: campaigns in this org are budget lines, not marketing campaigns. And until September 2026, leads were mostly a way to enter a deal, not a real funnel. Six metrics passed validation. Three open questions go to reviewers, each with the default I used.

**What I found**
- **Lead status:** "Qualified" means the same as converted (46 of 46 converted leads, and no unconverted lead is Qualified). "New Lead" is used only by a bulk import on 2026-09-01. In that import one user loaded 100 leads at once, all marked Referral - Team and USD. They make up 100 of the 143 leads created in 2026 Q3.
- **Leads before the import:** 33 of the 41 converted leads were converted the same day they were created. Every lead created from 2025 Q3 through 2026 Q2 is converted. The org's conversion-rate reports therefore show close to 100% before 2026 Q3, which reflects how deals were entered rather than lead quality.
- **Junk records:** there are 6 test leads (5 converted) and 6 leads created with the org on 2025-01-20. They look like Salesforce's own sample data.
- **What conversion produces:** mostly new accounts and top-level deals (Master Opportunities: 11 lost, 3 won, 17 open), plus 5 project-level Sales Opportunities. Two converted leads point to opportunities that are no longer in the snapshot.
- **Deal amounts from converted leads:** these are dominated by lost deals (92,000,000 lost in total, with single deals of 27,000,000 and 23,000,000). The "Leads Converted" reports sum this amount, so it is not revenue.
- **Lead source on deals:** only deals that came from a converted lead have a lead source. 144 Master Opportunities have none, so pipeline by lead source isn't supported.
- **Campaign structure:** one 2025 tree runs from the root to 6 client nodes to 18 service-line leaves. There are no campaign members, and only Master Opportunities are tagged to campaigns.
- **Budget double counting:** the budget and net revenue are entered on the leaves and repeated on the root, and on the "New Business" node. Adding up all campaigns (as the Dashboard - Revenue Budget report's grand total does, 44,117,707.49) counts the budget two or three times. The leaves alone give the correct 20,016,974.
- **Won value on campaigns:** Salesforce's won total on the campaigns (18,797,607.02) includes 4 deals won in 2026 (4,416,000). 37 of the 42 Master Opportunities won in 2025 are tagged to a campaign, but only 4 of the 20 won in 2026. There is no 2026 budget tree.

**Metrics drafted (FY2025 results)**

| Metric | FY2025 | Definition |
|---|---|---|
| `leads_created` | 29 | All leads, by created date |
| `leads_converted` | 23 | Converted leads, by conversion date |
| `leads_converted_of_created` | 23 | Leads created in the period that have since converted |
| `lead_conversion_rate` | 79.3% | The line above divided by leads created, matching the org's Conversion Rate report |
| `campaign_revenue_budget` | 20,016,974 | Budget on leaf campaigns only |
| `campaign_won_value` | 18,797,607.02 | Salesforce's won total on the leaf campaigns |
| `revenue_budget_attainment` | 93.9% | Won value divided by budget, matching the Dashboard - Revenue Budget report's % formula |

The two lead count metrics are set to reconcile against the org's reports; the compile step didn't report a reconciliation result for either. The campaign metrics use each campaign's created date to place it in a year, which puts the whole budget tree in FY2025.

I also added 2 glossary terms (Campaign as a budget line; Qualified means converted) and 4 gotchas (budget double counting, the September import, converted-deal amounts not being revenue, and leads as a data-entry path).

**Open questions (default used in brackets)**
1. Should attainment count wins that closed in 2026 but are tagged to 2025 campaigns? Counting only 2025 closes gives about 72% instead of 94%. [Count them, as the campaign totals and the dashboard do.]
2. Should the September import, test leads and sample leads be excluded from lead counts? [No: count everything, as the org's reports do, and flag these records instead.]
3. How should budget years be identified once a 2026 campaign tree exists? [Use the campaign's created date for now.]

**Not drafted:**
- A converted-deal amount metric, because the amounts are unreliable (see the lost-deal point above).
- Campaign member, response or cost metrics, because no members exist and the cost fields are empty on all 25 campaigns.
- A net-revenue budget metric. It could be built the same way as the gross budget, but I didn't draft it.
- **activity**: 31 turns. Activity topic (snapshot 2026-09-29)

Established:
- 11 sample tasks and 3 sample events came from org setup (creator 005Kc0000010gjJIAQ, 2025-01-20); they are excluded everywhere. That leaves 102 real tasks and 10 real events.
- 56 of the 102 real tasks are "Follow-up after Presentation" reminders made by the flow Opportunity_AS_Follow_up_Task. Each is due the day it was created, 51 are open and overdue, and most sit on opportunities that are already closed. Because the flow fired during the opportunity bulk load, it caused the May 2025 task spikes.
- 31 open next-step tasks were loaded on 2026-07-08 ET (07-09 UTC). None has a due date, so metrics dated by due date never count them.
- TaskRelation and EventRelation only repeat each activity's primary Who and What (the contact/lead and the related record), so joins don't double count. Every task on an opportunity has the same owner and account as that opportunity.
- Role: UserRoleId is never filled and Title is nearly empty, so the owner's profile is the only role signal. It is used as a proxy through Owner.ProfileId, with profile ids mapped to names in the notes.
- Events: ActivityDate is the start date in the org time zone (2 of 10 events fall on a different UTC date). Event Type is empty and all 10 real events are in 2026. Two zero-length "Audio" notes on a record that isn't an opportunity are excluded.

Metrics drafted and passing (FY2025 value, all checked by hand with SQL):
- tasks_completed: 8
- tasks_by_due_date: 54
- meetings_held: 0
- total_activities (derived, tasks_by_due_date + meetings_held): 54
- opportunities_with_activity: 49. Opportunities are identified by the WhatId key prefix 006 because the What relationship can't be joined. Only 2 of these opportunities have a task a person created.
- accounts_with_activity: 18. Only 3 of these accounts have a task that isn't the automated follow-up.

Open:
- Question: should the automated follow-ups count as activity? Default: included, with a caveat in each metric.
- Question: is profile the right role proxy? Default: Owner.ProfileId.
- None of the metrics were reconciled to the org's reports, because those reports are grouped by person or dated by Account.CreatedDate or CloseDate.
- No open or overdue task backlog metric was drafted, because the automated follow-ups make it misleading until the first question is answered.

## Metric values at sweep time

- `tasks_completed` FY2025: 8
- `meetings_held` FY2025: 0
- `leads_created` FY2025: 29
- `leads_converted` FY2025: 23
- `opportunities_with_activity` FY2025: 49
- `push_revenue` FY2025: 1707070.92
- `engagements_by_close_date` FY2025: 53
- `push_revenue_margin` FY2025: 0.12906549102944777893
- `leads_converted_of_created` FY2025: 23
- `open_pipeline_amount` FY2025: 0
- `lead_conversion_rate` FY2025: 0.79310344827586206897
- `lost_count` FY2025: 10
- `new_business_won_count` FY2025: 3
- `new_business_closed_count` FY2025: 11
- `gross_revenue_pipeline` FY2025: 42000
- `revenue_budget` FY2025: 20016974.49
- `tasks_by_due_date` FY2025: 54
- `new_business_win_rate` FY2025: 0.27272727272727272727
- `campaign_revenue_budget` FY2025: 20016974
- `clients_won` FY2025: 9
- `total_activities` FY2025: 54
- `open_pipeline_count` FY2025: 1
- `open_engagements` FY2025: 1
- `campaign_won_value` FY2025: 18797607.02
- `accounts_with_activity` FY2025: 18
- `revenue_budget_attainment` FY2025: 0.93908335096004021387
- `project_pipeline_amount` FY2025: 42000
- `weighted_pipeline_amount` FY2025: 0
- `open_pipeline_amount_p10` FY2025: 0
- `open_pipeline_amount_p25` FY2025: 0
- `open_pipeline_amount_p50` FY2025: 0
- `open_pipeline_amount_p75` FY2025: 0
- `open_pipeline_amount_p90` FY2025: 0
- `pushed_open_engagements` FY2025: 0

## Dropped

- nothing

## Deterministic anomalies

- bulk_load · Account.CreatedDate: 46 records created on 2026-07-08
- bulk_load · Account.CreatedDate: 27 records created on 2025-03-19
- dead_field · AccountContactRelation.Relationship_Strength__c: custom field never filled in 75 records
- bulk_load · AccountContactRelation.CreatedDate: 18 records created on 2026-07-08
- bulk_load · Contact.CreatedDate: 18 records created on 2026-07-08
- bulk_load · Lead.CreatedDate: 100 records created on 2026-09-01
- dead_field · Opportunity.Proposal_Hours__c: custom field never filled in 359 records
- concentration · Opportunity.Media_Spend_1stMo__c: one record holds 23.8% of the Media_Spend_1stMo__c total
- concentration · Opportunity.Media_Spend_2ndMo__c: one record holds 27.1% of the Media_Spend_2ndMo__c total
- concentration · Opportunity.Media_Spend_3rdMo__c: one record holds 39.8% of the Media_Spend_3rdMo__c total
- concentration · Opportunity.Media_Spend_4thMo__c: one record holds 39.8% of the Media_Spend_4thMo__c total
- concentration · Opportunity.Media_Spend_5thMo__c: one record holds 41.2% of the Media_Spend_5thMo__c total
- concentration · Opportunity.Media_Spend_6thMo__c: one record holds 48.7% of the Media_Spend_6thMo__c total
- concentration · Opportunity.Media_Spend_7thMo__c: one record holds 100.0% of the Media_Spend_7thMo__c total
- concentration · Opportunity.Media_Spend_8thMo__c: one record holds 100.0% of the Media_Spend_8thMo__c total
- concentration · Opportunity.Media_Spend_9thMo__c: one record holds 100.0% of the Media_Spend_9thMo__c total
- concentration · Opportunity.Total_Media_Spend__c: one record holds 25.4% of the Total_Media_Spend__c total
- dead_field · Opportunity.Commission_Percent__c: custom field never filled in 359 records
- money_gaps · Opportunity.Sum_of_Sales_Opportunities__c: 317 of 359 records have no Sum_of_Sales_Opportunities__c
- money_gaps · Opportunity.Vendor_Cost__c: 341 of 359 records have no Vendor_Cost__c
- concentration · Opportunity.Vendor_Cost__c: one record holds 27.9% of the Vendor_Cost__c total
- concentration · Opportunity.PUSH_Revenue__c: one record holds 27.3% of the PUSH_Revenue__c total
- dead_field · Opportunity.Commission_Lump_Amount__c: custom field never filled in 359 records
- dead_field · Opportunity.Vendor__c: custom field never filled in 359 records
- concentration · Opportunity.Spent_Amount__c: one record holds 20.7% of the Spent_Amount__c total
- dead_field · Opportunity.Teamwork_ID__c: custom field never filled in 359 records
- money_gaps · Opportunity.Fees_Amount__c: 154 of 359 records have no Fees_Amount__c
- money_gaps · Opportunity.Sum_of_Fees__c: 317 of 359 records have no Sum_of_Fees__c
- concentration · Opportunity.Sum_of_Fees__c: one record holds 25.6% of the Sum_of_Fees__c total
- money_gaps · Opportunity.Sum_of_Media_Spend__c: 317 of 359 records have no Sum_of_Media_Spend__c
- concentration · Opportunity.Sum_of_Media_Spend__c: one record holds 33.4% of the Sum_of_Media_Spend__c total
- bulk_load · Opportunity.CreatedDate: 76 records created on 2026-07-08
- money_gaps · OpportunityHistory.PrevAmount: 400 of 732 records have no PrevAmount
- bulk_load · OpportunityHistory.CreatedDate: 128 records created on 2025-05-27
- bulk_load · OpportunityHistory.CreatedDate: 76 records created on 2026-07-08
- bulk_load · OpportunityFieldHistory.CreatedDate: 128 records created on 2025-05-27
- bulk_load · OpportunityFieldHistory.CreatedDate: 76 records created on 2026-07-08
- bulk_load · OpportunityFieldHistory.CreatedDate: 75 records created on 2026-01-09
- money_gaps · Opportunity__hd.Amount__hpr: 320 of 630 records have no Amount__hpr
- bulk_load · Opportunity__hd.CreatedDate: 76 records created on 2026-07-08
- bulk_load · Opportunity__hd.CreatedDate: 63 records created on 2025-12-17
- bulk_load · Opportunity__hd.CreatedDate: 60 records created on 2025-05-27
- bulk_load · OpportunityContactRole.CreatedDate: 50 records created on 2026-07-08
- concentration · Campaign.ExpectedRevenue: one record holds 45.4% of the ExpectedRevenue total
- money_gaps · Campaign.BudgetedCost: 25 of 25 records have no BudgetedCost
- money_gaps · Campaign.ActualCost: 25 of 25 records have no ActualCost
- concentration · Campaign.AmountAllOpportunities: one record holds 87.0% of the AmountAllOpportunities total
- concentration · Campaign.AmountWonOpportunities: one record holds 27.3% of the AmountWonOpportunities total
- money_gaps · Campaign.Net_Revenue__c: 6 of 25 records have no Net_Revenue__c
- concentration · Campaign.Net_Revenue__c: one record holds 50.0% of the Net_Revenue__c total
- bulk_load · Task.CreatedDate: 31 records created on 2026-07-08
- bulk_load · Task.CreatedDate: 20 records created on 2025-05-13
- bulk_load · TaskRelation.CreatedDate: 31 records created on 2026-07-08
- bulk_load · TaskRelation.CreatedDate: 20 records created on 2025-05-13
- dead_field · Monthly_Revenue_Plan__c.Hard_Costs_Actual__c: custom field never filled in 45 records
- dead_field · Monthly_Revenue_Plan__c.Creative_Fees_Planned__c: custom field never filled in 45 records
- dead_field · Monthly_Revenue_Plan__c.Creative_Fees_Actual__c: custom field never filled in 45 records
- money_gaps · Monthly_Revenue_Plan__c.Media_Fees_Actual__c: 38 of 45 records have no Media_Fees_Actual__c
- concentration · Monthly_Revenue_Plan__c.Fees_Actual__c: one record holds 23.1% of the Fees_Actual__c total
- concentration · Monthly_Revenue_Plan__c.Total_Actual__c: one record holds 23.1% of the Total_Actual__c total
- tracked_changes · Opportunity.created: 324 changes on 324 records (2025-04-07 to 2026-09-21)
- tracked_changes · Opportunity.Amount: 211 changes on 126 records (2025-05-13 to 2026-09-29)
- tracked_changes · Opportunity.StageName: 141 changes on 106 records (2025-04-07 to 2026-09-29)
- tracked_changes · Opportunity.Media_Spend_1stMo__c: 68 changes on 45 records (2025-04-07 to 2026-09-02)
- tracked_changes · Opportunity.Media_Spend_2ndMo__c: 43 changes on 33 records (2025-04-07 to 2026-09-02)
- tracked_changes · Opportunity.opportunityCreatedFromLead: 35 changes on 35 records (2025-06-18 to 2026-09-17)
- tracked_changes · Opportunity.Media_Spend_3rdMo__c: 29 changes on 21 records (2025-04-07 to 2026-09-02)
- entered_closed · Opportunity.StageName: 77 opportunities first recorded already at closed stage Project Completion
- entered_closed · Opportunity.StageName: 72 opportunities first recorded already at closed stage Project In Progress
- entered_closed · Opportunity.StageName: 27 opportunities first recorded already at closed stage Closed Won
- entered_closed · Opportunity.StageName: 6 opportunities first recorded already at closed stage Closed Lost

## Review

All metrics are `status: proposed`. Accept one by changing its status to `accepted` in a reviewed commit; Plum only serves verified answers from accepted metrics.
Report-faithful metrics are not yet reconciled against live report runs (M6).

Tokens: 319421 input, 6450176 cached input, 138643 output.

# Gotchas

Traps that give wrong numbers.

## KPI revenue reports use retired won stages and miss Closed Won
Gross Revenue - Total, PUSH Revenue - Total/Monthly, and the BD 'Won Opportunities' reports filter StageName to Financial Setup/Kick-off/Project In Progress/Project Completion. Those stages are now inactive, and wins from 2026-07 onward go to Closed Won. For FY2026 the stage filter shows 1 of 21 won projects (348,893.2 CAD instead of 1,799,873 CAD gross). Use IsWon = true.

Evidence: `q33`, `q66`, `q17` (see findings/).
  > Reviewer: 'Wins from 2026-07 onward go to Closed Won' misstates the timing. Field history (q66) shows moves into Closed Won starting 2026-07. But q19 shows Closed Won records with CloseDates from 2026-01-23 (CAD) and 2026-03-31 (USD). These were probably created directly in Closed Won or migrated without history. The stage filter misses essentially all FY2026 wins, not just those after July. It catches only the single Project In Progress record. Reword and add the PUSH-revenue effect (0 vs 894,924 CAD).

## PUSH Revenue is 0 on Media projects without a fee % or media spend
For Media, PUSH_Revenue__c = Total_Media_Spend__c × Media_Fee__c. 34 of the 67 won CAD Media projects and all 7 won USD Media projects have PUSH revenue of 0 because the fee % is blank or monthly spend was never entered. Net revenue for Media is understated. Fees_Amount__c is not a substitute, because on most Media projects it equals the gross Amount.

Evidence: `q8`, `q28` (see findings/).
  > Reviewer: Same gap as c102. 4 zero-PUSH CAD Media records, including 3 in FY2025 with 3.4M of media spend, have both a fee % and spend filled in, so 'fee % is blank or spend never entered' does not explain them (likely a 0% fee). Add that case. 'Most' for Fees_Amount__c = Amount is thin: 39 of 67 CAD Media and 0 of 7 USD, so 39 of 74 overall.

## 'Special Project' opportunity type no longer exists
The report 'PUSH Revenue - Special Projects' (00OKc0000014dXcMAI) filters Type = 'Special Project', but opportunities only use Media, Creative and Agency, so the report returns nothing. The budget campaigns still name a 'Special Projects' service line. It most likely corresponds to Type = Agency, but that is unconfirmed.

Evidence: `q8`, `q47` (see findings/).
  > Reviewer: The evidence (q8) covers only won Sales Opportunities. It does not show that no opportunity uses 'Special Project': open and lost Sales Opps and Master Opportunities are not checked, and neither is the Type picklist. The budget 'Special Projects' leaves have won master opportunities tagged (for example Pharmacare with 2 wins and 174,000), so masters may carry a different Type. Run a Type distribution across all record types and statuses before saying the report returns nothing, and before mapping Special Projects to Agency by default.

## USD projects start in FY2026; conversion uses one static rate
All USD won projects are Push USA wins in FY2026 (16 won, 729,173 USD). The org has no dated exchange rates: CAD = USD / 0.737. Mixing native-currency Amounts without conversion overstates the CAD total less than it looks but is still wrong. Also, 3 Push USA wins are recorded in CAD, and 1 won project has a CloseDate after the snapshot date. Revenue is dated by CloseDate, and most FY2024–FY2025 projects were backfilled after their close date.

Evidence: `q81`, `q19` (see findings/).
  > Reviewer: The direction is wrong. At 0.737 USD per CAD, 1 USD is about 1.357 CAD, so adding native USD Amounts as if they were CAD understates the CAD total (for FY2026, 729,173 in place of about 989,380). It does not overstate it. The rest is supported by q81/q19: the 16 USD Push USA wins, the 3 CAD Push USA wins, 1 CloseDate after 2026-09-29 (max 2026-10-31), and the FY2024–25 backfill.

## BD "won" reports miss Closed Won
The PUSH KPI won reports filter on stages Kick-off, Project In Progress, Project Completion and leave out Closed Won. For FY2025 engagements they show 41 wins vs 42 by IsWon; for FY2026 they show 0 vs 20, because every FY2026 win is Closed Won. Always define won by IsWon.

Evidence: `q9` (see findings/).
  > Reviewer: This has the same issue as c106. The counts are right, but the report filter itself (stages only, no Closed Won) is not shown in any attached evidence. Attach the report metadata or mark the filter as unverified.

## Win rate is inflated by backfilled wins, and by existing clients
Most FY2025 engagement wins were loaded already at a won stage. Engagements that entered the pipeline open went 3 won / 8 lost in FY2025 and 5 / 5 in FY2026. Existing-client engagements won 39 of 41 in FY2025, new business 3 of 11. Quote new_business_win_rate alongside win_rate.

Evidence: `q32`, `q34` (see findings/).

## Engagement Amount is dominated by huge lost bids
The BD KPI reports sum Amount on Master Opportunities, but that total is dominated by a few very large RFP bids that were lost. One 27,000,000 CAD lost engagement is 60.3% of FY2026 decided engagement value. Do not compute amount-weighted win rates, and do not treat engagement Amount as revenue; revenue comes from won projects (gross_revenue).

Evidence: `q50`, `q53` (see findings/).

## Salesforce sample activities from org setup
11 tasks (subjects end in "(Sample)", e.g. call reminders) and 3 events were created on 2025-01-20 by the org-creating user 005Kc0000010gjJIAQ. They are demo data. Exclude them with CreatedById != 005Kc0000010gjJIAQ; that user created no other activity.

Evidence: `q37` (see findings/).
  > Reviewer: Only 10 of the 11 tasks have '(Sample)' in the subject, and 1 of the 3 events has no '(Sample)' in its subject either (q37). Say that one task and one event lack the marker, and that the exclusion relies on CreatedById, not the subject.

## Automated "Follow-up after Presentation" tasks dominate task counts
The flow Opportunity_AS_Follow_up_Task makes a task "Follow-up after Presentation <opportunity>", due the day it is created, when an opportunity reaches presentation. 56 of the 102 real tasks are these reminders, 51 are open and past due, and most sit on opportunities that are already closed. Because they fired during the May 2025 opportunity bulk load, the 2025-05-13/14 task spikes are an artifact. Any "open tasks", "overdue tasks" or "opportunities with activity" number is mostly these reminders; split by subject prefix when you need human activity.

Evidence: `q11`, `q40`, `q20`, `q115` (see findings/).
  > Reviewer: 'Because they fired during the May 2025 opportunity bulk load' is not supported by the evidence (see c75): no query examines when opportunities were created. The rest holds: 56 of 102, 51 open and past due, and in fact all 56 sit on closed opportunities (q20). Drop the bulk-load cause or add evidence for it.

## 31 next-step tasks loaded 2026-07-08 have no due date
One user loaded 31 open tasks at 2026-07-08 ET (2026-07-09 UTC), one per opportunity, with next-step notes as subjects and no ActivityDate. Metrics dated by due date never include them; they only show up in "all open tasks" lists. Group by the org time zone date, not UTC, or the load moves to 07-09.

Evidence: `q7` (see findings/).

## Campaign budget is entered at several levels — sum leaves only
ExpectedRevenue and Net_Revenue__c appear on the root "2025" campaign (20,016,974.49 / 4,201,683.64), on the leaves (20,016,974 / 4,201,683.64), and the "New Business" client node repeats its leaves (4,083,759). Summing all campaigns (as the Dashboard - Revenue Budget report's grand total does) counts the budget two to three times. Filter to campaigns whose Parent.ParentId is not null.

Evidence: `q42`, `q25` (see findings/).

## lead-bulk-import-2026-09: 100 leads loaded in one insert
On 2026-09-01 21:32:44 UTC one user inserted 100 leads (all Referral - Team, USD, distinct large-brand companies); 96 are still 'New Lead'. They are 100 of 143 leads created in 2026 Q3 and make 'Referral - Team' the dominant lead source. Any lead-volume, by-source or conversion-rate trend across 2026 is driven by this import.

Evidence: `q6`, `q10`, `q48` (see findings/).

## lead-converted-opportunity-amount: not revenue
The Leads Converted reports sum 'Opportunity Amount' of converted opportunities. These are mostly Master engagements (estimates), many lost: 11 lost converted engagements total 92,000,000, with single amounts of 27,000,000 and 23,000,000. Leads converted in 2025 Q3 alone carry 68,617,700. Never use this as revenue or pipeline value without restricting to open/won and understanding engagement vs project.

Evidence: `q16`, `q21`, `q55` (see findings/).

## Leads were an entry path, not a funnel (before Sept 2026)
33 of 41 converted organic leads were converted the same day they were created, and 2025 Q3 through 2026 Q2 cohorts are 100% converted. Lead conversion rate before 2026 Q3 reflects data-entry habit, not qualification. Also only engagements created through conversion have Opportunity.LeadSource; 144 Master Opportunities have none, so pipeline-by-lead-source is not supported.

Evidence: `q10`, `q48`, `q63` (see findings/).
  > Reviewer: The note is titled 'before Sept 2026', but the 33-of-41 same-day figure covers organic leads converted through 2026-09-17. About 15 of those conversions are post-import 2026 Q3 leads, so the pre-import share was not measured. Also, 2025 Q1–Q2 cohorts were not 100% (3/8 and 4/5). Qualify the statement or re-run with CreatedDate < 2026-09-01.

## Pipeline double counts if you add Master and Sales opportunities
Open pipeline exists on both record types: engagements (Master_Opportunity) and projects (Sales_Opportunity). 39 open projects are children of open engagements, and an engagement's Amount is its own gross estimate, not a roll-up (22 open engagements with children: 12,165,496 on the engagement vs 6,884,901 on the children). Always pick one grain. Engagement pipeline = open_pipeline_amount. Project pipeline = project_pipeline_amount. Never add them.

Evidence: `q13`, `q29` (see findings/).
  > Reviewer: This has the same flaw as c94. The 6,884,901 'on the children' includes 26 closed children (4,906,615). Only 1,978,286 of open child pipeline overlaps with open engagement pipeline. 'Not a roll-up' should mention the Sum_of_Sales_Opportunities__c rollup (6,369,414), which exists but differs from the child sum. It should also mention that open engagements carry won child projects.

## KPI reports use stage names that no longer match the process
Forecast - Total, PUSH Revenue - Forecast Amount and Gross Revenue - Forecast Amount filter on 'Presentation', which is not a stage (the stage is 'Creds Presentation'), so 8 open engagements are dropped. The BD won reports filter won as 'Kick-off, Project In Progress, Project Completion'. Since the 2026-06-08 process change, wins are recorded as 'Closed Won' (all 20 FY2026 won engagements), so those reports show almost no FY2026 wins. Forecast - Total also puts won delivery stages at 100% into its 'forecast'. Define open as IsClosed = false and won as IsWon = true, not by stage lists.

Evidence: `q64`, `q67`, `q4` (see findings/).
  > Reviewer: Report filters are not in the evidence. PUSH Revenue and Gross Revenue - Forecast Amount are Sales Opportunity reports, and open Sales have no Creds Presentation records, so they do not drop the 8 open engagements. Only a Master-based report would. For Masters, q67 shows zero (not 'almost no') FY2026 wins in legacy stages, so a Master BD won report would show none. The general advice (IsClosed/IsWon) is sound.

## Stage history starts mid-stream for most records (entered closed)
In OpportunityHistory, 60 engagements and more than 120 projects have a closed stage as their first row (loaded or backfilled already won or lost). Another 20 engagements were first recorded at Contract (2026-09-14/15) and 22 at Proposal. Stage-conversion, stage-duration and sales-cycle metrics built from history must exclude records whose first stage is closed, and should report how many records started past Discovery. Regressions are rare (Masters: 7 backward moves on 3 deals). Moves between won stages (Project In Progress -> Project Completion) are delivery updates, not sales progress.

Evidence: `q36`, `q43` (see findings/).

## Collaborative Forecasting and quotas are not a usable forecast source
ForecastingItem and ForecastingFact cover only a handful of opportunities for up to 3 owners, mix engagements and projects, and have no adjustments. ForecastingQuota has 6 stale rows. Compute forecasts from Opportunity (forecast category and probability), not from the forecasting objects. Pipeline coverage against quota cannot be computed; Monthly_Revenue_Plan__c may be the real plan (not investigated here).

Evidence: `q58`, `q59` (see findings/).
  > Reviewer: 'ForecastingQuota has 6 stale rows' and 'no adjustments' have no supporting query in the evidence (only ForecastingFact and ForecastingItem were queried). Either add the quota and adjustment queries or remove or soften those statements. The rest (few opportunities, at most 3 owners, mixed record types) is supported.

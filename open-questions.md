# Open questions

Choices the sweep could not settle from the data. The ontology uses the default until someone answers.

## Q1. Is the revenue budget measured against engagements or projects?
The 2025 revenue budget (Campaign ExpectedRevenue, 20,016,974.49 CAD) is compared in 'Dashboard - Revenue Budget Report' to Master Opportunity Amount, and in 'Dashboard - Revenue Budget PUSH' to won Sales Opportunity Amount. FY2025 won masters total 19,948,445.47 CAD and won projects 13,226,393.10 CAD, so attainment is roughly 100% or roughly 66% depending on the choice. Budget lines are tagged only on Master Opportunities.

**Default:** Attainment = gross_revenue (won Sales Opportunities, CAD) / revenue_budget, consistent with money being summed on projects; no attainment metric drafted until confirmed.

Evidence: `q118`, `q54`

## Q2. Is "Organic Growth" new business or existing business?
Business_Type__c has four values. New and New - RFP are clearly new business and Exisiting is existing. Organic Growth (a few engagements, mostly FY2026/FY2027) could mean either expansion within a current client or new work that came in without a pursuit. The account for its one won engagement had no earlier win.

**Default:** Treated as existing business: excluded from new_business_won_count / new_business_closed_count.

Evidence: `q34`, `q39`
  > Reviewer: q39 shows all 4 Organic Growth engagements, not just the won one, sit on accounts with no earlier win: 3 never won, 1 first win the same day. That is evidence against reading Organic Growth as "expansion within a current client", yet the default treats it as existing business. The body should state this, and the default should be flagged as going against the available evidence (the impact is small: 1 win).

## Q3. Should win rate exclude wins that were entered already won?
Many engagements were created directly at a won stage (the backfill, and FY2026 Closed Won entries), while losses are rarely backfilled. A pipeline-conversion win rate that counts only engagements which entered the pipeline open would be about 3/11 for FY2025 instead of 42/52.

**Default:** No. win_rate counts all decided engagements (the accepted definition, golden G13); the backfill bias is documented as a caveat.

Evidence: `q32`

## Q4. Should automated presentation follow-ups count as sales activity?
Flow-generated "Follow-up after Presentation" tasks are 56 of 102 real tasks and almost all opportunity/account activity coverage in 2025. Metrics cannot filter by subject prefix, so they are included. Should activity metrics exclude them (e.g. via a flag field the flow sets), or count only once completed?

**Default:** Included in tasks_by_due_date, total_activities, opportunities_with_activity and accounts_with_activity; in tasks_completed only when completed. Caveated in each metric's notes.

Evidence: `q11`, `q115`, `q125`

## Q5. Which field defines a rep's role for activity reporting?
UserRoleId is never filled and only one standard user has a Title, so activity "by role" uses the owner's profile (Standard User, Client Service - Manager, Creative Services - Manager, Media Ops, System Administrator). Is profile the right proxy, or should roles/titles be filled in?

**Default:** Owner.ProfileId, with profile ids mapped to names in the metric notes.

Evidence: `q65`, `q14`

## Q6. Should budget attainment count 2026-closed wins tagged to 2025 campaigns?
The campaign rollup 'Value Won Opportunities' (18,797,607.02 for the 2025 tree) includes 4 engagements won in 2026 (4,416,000). Counting only 2025 closes gives 14,381,607.02, i.e. about 72% instead of 94% attainment against the 20,016,974 budget. Which is the intended actual?

**Default:** Use the Salesforce rollup as the Dashboard - Revenue Budget report does (all tagged wins regardless of close date), and state the 2026-closed portion in notes.

Evidence: `q46`, `q136`

## Q7. Exclude the Sept 2026 list import, test and seed leads from lead counts?
Lead reports count all leads. 100 leads came from one 2026-09-01 list import, 6 are Salesforce seed leads from org creation (2025-01-20) and 6 have test company names (5 converted). Should lead volume and conversion rate exclude any of these?

**Default:** Count all leads, like the org's reports; test leads and the import are flagged via coverage checks and notes, not excluded.

Evidence: `q6`, `q10`, `q51`
  > Reviewer: This item was cut off in the submitted batch, so its content and evidence could not be reviewed. Resubmit it.

## Q8. How should budget years be identified once a 2026 campaign tree exists?
Budget campaigns have no start/end dates below the root, so campaign metrics use CreatedDate (all 25 created 2025-12-17..19) to place the 2025 budget in FY2025. A 2026 tree created in late 2026 or early 2027 would land in the wrong year.

**Default:** Use Campaign.CreatedDate for now; revisit (e.g. root campaign name or StartDate) when a second budget tree appears.

Evidence: `q25`

## Q9. Is 'the pipeline' engagements (Master) or projects (Sales)?
Open engagement pipeline is roughly 61M native and open project pipeline roughly 2.2M. Forecast - Total and the BD reports use Master Opportunities; Gross Revenue - Forecast Amount and PUSH Revenue - Forecast Amount use Sales Opportunities. Which one should 'pipeline' mean when someone asks without saying?

**Default:** 'Pipeline' means engagement (Master_Opportunity) pipeline, open_pipeline_amount. Project pipeline (project_pipeline_amount) is used only when the question is about revenue forecast or projects.

Evidence: `q13`, `q29`, `q26`

## Q10. Weight pipeline by the deal's probability or by the stage default?
Reps override probability on some deals (e.g. Proposal engagements at 0%, 10% or 75% instead of 50%). For FY2026 Best Case engagements, weighting by record probability gives 12,658,680.12 CAD and weighting by stage default gives 13,973,680.12 CAD.

**Default:** Use the record's Probability, as Salesforce's Expected Revenue / Weighted Forecast does (weighted_pipeline_amount).

Evidence: `q82`, `q12`

## Q11. Should open deals with a past close date stay in pipeline?
At snapshot, open engagements with a close date already past: 1 dated 2025 (no amount) and 5 dated 2026. Open projects: 1 dated 2025 and 5 dated 2026. They are still open in Salesforce but are probably stale.

**Default:** Keep them in pipeline in their original close-date period, as Salesforce does, and flag them with the close_date_before_snapshot coverage check rather than excluding them.

Evidence: `q26`

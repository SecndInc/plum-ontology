# Findings: Pipeline and forecast

I defined open pipeline at the engagement level (Master Opportunities not yet won or lost), gave project pipeline its own metric, and built a weighted pipeline. The weighted one needs a workaround and will break if reps start using new probability values.

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

## Claims

- **anomaly** (high) Summing open pipeline across both record types double counts: 39 open Sales Opportunities are children (Parent_Opportunity__c) of open Master Opportunities. Of 81 open Masters, 22 have child Sales opportunities; their Master Amount totals 12165496 while all their children total 6884901 (native currency), so Master amount and child amounts are different estimates of the same engagement, not additive. — `q13`, `q29`
  > Reviewer: The 6,884,901 'children' total in q29 has no IsClosed filter on the kids CTE, so it counts every child of the 22 open Masters. q13 splits it: 1,978,286 from 39 open children and 4,906,615 from 26 closed children. The actual double count when you add open pipeline across both record types is only the 1,978,286 of open child Sales. The claim should also say that open Masters have 26 closed (mostly won-stage) child projects. So an open engagement Amount may partly cover value already booked as won on the Sales side. 'Different estimates of the same engagement' is an interpretation. There is also a rollup field (Sum_of_Sales_Opportunities__c = 6,369,414) that does not match the child sum, and that gap should be noted.
- **fact** (high) Forecast category always follows the stage for open Masters (Discovery/Creds Presentation = Pipeline, Proposal = Best Case, Contract = Commit). Probability is not always the stage default: 8 open Master Proposals carry 0% (3, amount 0), 10% (1, 3750000) or 75% (4, 6390000) instead of 50%; open Sales opportunities deviate more (Discovery at 25% or 50%, Proposal at 25/75/80/90%, 2 Contracts at 50%), and one Sales Contract is in Best Case instead of Commit. — `q12`
- **fact** (high) Open engagement (Master) pipeline closing in FY2026, in CAD (USD / 0.737): Best Case 18 deals 27947360.24 (weighted by record Probability 12658680.12; by stage default 13973680.12), Commit 23 deals 15595996 (weighted 14036396.4), Pipeline 6 deals 100000 (weighted 10000). FY2027: Best Case 5 deals 6950000 (weighted 4887500), Pipeline 28 deals 17313297.15 (weighted 2783385.35). 5 FY2026 Best Case Masters have no Amount. — `q82`
- **fact** (high) Only two Opportunity record types hold data: Master_Opportunity (012Kc000000xcSYIAY, engagements) and Sales_Opportunity (012Kc000000xd9cIAA, projects); the Stratis record type has no records. Open Masters by stage: Discovery 27, Creds Presentation 8, Proposal 23, Contract 23. Open Sales by stage: Discovery 17, Proposal 25, Contract 3 in Commit plus 1 in Best Case. Open Sales opportunities have no Creds Presentation or Negotiation records. — `q4`
- **anomaly** (high) Open engagement pipeline is concentrated: in FY2026 close dates, 47 open Masters total 38273196 (native currency) and the largest single Master is 15000000 of it. Across all open Masters 61323196 native, largest 15000000. — `q26`, `q29`
- **fact** (high) Stage regressions are rare: using the order Discovery < Creds Presentation < Proposal < Negotiation < Contract, Masters had 7 backward moves on 3 opportunities and 1 reopen from a closed stage; Sales had 3 backward moves on 3 opportunities. 3 opportunities moved from a won stage to Closed Lost (Master 2, Sales 1). Moves between won stages (e.g. Project In Progress -> Project Completion) are delivery status, not sales progress: 11 on Masters, 29 on Sales. — `q43`
  > Reviewer: won_to_lost is COUNTIF over moves, not distinct opportunities, so '3 opportunities moved from a won stage to Closed Lost' is not shown. It is 3 moves, and one opportunity could account for both Master moves. The ELSE 6 bucket also puts every unlisted stage in the 'won' group (Qualification, Needs Analysis, Financial Setup, Stratis stages). 'won_to_won' and 'reopened from a closed stage' may therefore include non-won stages. History order ties (same CreatedDate) are broken by Id, which may not be chronological.
- **fact** (high) Close-date slippage is concentrated in September 2026: 29 open Masters had their close date moved 31 times, 30 of them later (net +5744 days), and PushCount (30) matches the month-crossing pushes found in OpportunityHistory. On 2026-09-21 (org time) 12 open Masters were pushed from 2026 into 2027, plus further pushes on 2026-09-09 (3), 2026-09-10 (2) and 2026-09-01 (1) from 2026 into 2027. — `q49`, `q52`
- **anomaly** (high) Many opportunities were entered already closed (first OpportunityHistory row at a closed stage). Masters: Project In Progress 36, Closed Won 15, Project Completion 5, Closed Lost 4. Sales: Project Completion 72, Project In Progress 36, Closed Won 12, Kick-off 4, Closed Lost 2. Also 20 Masters were first recorded at Contract on 2026-09-14/15 and 22 at Proposal from 2026-07-09, so they never passed through earlier stages in the history. — `q36`
- **anomaly** (medium) The sales process changed on 2026-06-08: Creds Presentation was created that day and Kick-off, Project In Progress, Project Completion and Financial Setup were deactivated (last modified 2026-06-08). Since then wins use Closed Won: all 20 FY2026 won Masters and 20 of 21 FY2026 won Sales are at Closed Won. Reports that filter won by "Kick-off, Project In Progress, Project Completion" (BD won reports) or open by "Discovery, Presentation, ..." (Forecast - Total, Gross Revenue - Forecast Amount) therefore miss Closed Won deals and the 8 open Creds Presentation Masters. Stages Initial Outreach..Pilot Active were created 2026-08-24, apparently for the Stratis record type, which has no records. — `q64`, `q67`, `q4`
  > Reviewer: No report definitions are in the evidence, so the claims about BD won reports and the 'Presentation' filter are not verified here. Gross Revenue - Forecast Amount is a Sales Opportunity report (see project_pipeline_amount/n159), and open Sales have no Creds Presentation records, so it does not miss the 8 Creds Presentation Masters. FY2026 wins include deals closed before 2026-06-08, and Closed Won Masters were created from 2025-10. 'Since then' is therefore not isolated by the query. The deactivation date is inferred from LastModifiedDate. The Stratis link for the new stages is speculation.
- **caveat** (medium) Collaborative Forecasting is barely used and cannot be the forecast source: all ForecastingItems belong to one forecasting type (0DbKc000000gPCiKAM) with at most 3 owners, ForecastingFacts link only a handful of opportunities mixing both record types (e.g. Master Closed 7 opps, Sales Closed 6 opps), and none carry adjustments. Forecast quotas are not usable for pipeline coverage. — `q58`, `q59`
  > Reviewer: q58/q59 support one forecasting type, at most 3 owners and only a handful of linked opportunities. No query looks at adjustments (ForecastingAdjustment or adjustment fields) or at ForecastingQuota, so 'none carry adjustments' and 'quotas are not usable' have no evidence. Also, ForecastingItems were still being modified on 2026-09-29, which weakens 'barely used'. Say it covers little of the pipeline instead.

## Evidence queries

Each runs with `@snapshot_run_id` set to the snapshot below and returned the rows summarised here.

### q13: Parent/child relationship between Master and Sales opportunities, open vs closed
```sql
SELECT o.RecordTypeId, o.IsClosed, p.RecordTypeId parent_rt, p.IsClosed parent_closed, COUNT(*) n, COUNTIF(o.Parent_Opportunity__c IS NULL) no_parent, SUM(o.Amount) amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` p ON p.Id=o.Parent_Opportunity__c AND p._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id
GROUP BY 1,2,3,4 ORDER BY 1,2,3,4
```
8 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","IsClosed":false,"parent_rt":null,"parent_closed":null,"n":81,"no_parent":81,"amt":"61323196"},{"RecordTypeId":"012Kc000000xcSYIAY","IsClosed":true,"parent_rt":null,"parent_closed":null,"n":81,"no_parent":81,"amt":"128646603.47"},{"RecordTypeId":"012Kc000000xd9cIAA","IsClosed":false,"parent_rt":null,"parent_closed":null,"n":7,"no_parent":7,"amt":"237000"},{"RecordTypeId":"012Kc000000xd9cIAA","IsClosed":false,"parent_rt":"012Kc000000xcSYIAY","parent_closed":false,"n":39,"no_parent":0,"amt":"1978286"},{"RecordTypeId":"012Kc000000xd9cIAA","IsClosed":true,"par`
### q29: Master vs child Sales amounts
```sql
WITH kids AS (SELECT Parent_Opportunity__c pid, COUNT(*) nk, SUM(Amount) kid_amt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND Parent_Opportunity__c IS NOT NULL GROUP BY 1)
SELECT m.IsClosed, COUNT(*) masters, COUNTIF(k.pid IS NOT NULL) with_kids, SUM(m.Amount) master_amt, SUM(IF(k.pid IS NOT NULL, m.Amount, 0)) master_amt_with_kids, SUM(k.kid_amt) kid_amt, SUM(m.Sum_of_Sales_Opportunities__c) rollup_amt,
 MAX(m.Amount) max_amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` m LEFT JOIN kids k ON k.pid=m.Id
WHERE m._run_id=@snapshot_run_id AND m.RecordTypeId='012Kc000000xcSYIAY' GROUP BY 1
```
2 rows; first rows: `[{"IsClosed":true,"masters":81,"with_kids":24,"master_amt":"128646603.47","master_amt_with_kids":"17517040.45","kid_amt":"13697303.79","rollup_amt":"12704510.65","max_amt":"27000000"},{"IsClosed":false,"masters":81,"with_kids":22,"master_amt":"61323196","master_amt_with_kids":"12165496","kid_amt":"6884901","rollup_amt":"6369414","max_amt":"15000000"}]`
### q12: Open opps: probability and forecast category vs stage defaults
```sql
SELECT o.RecordTypeId, o.StageName, o.Probability, s.DefaultProbability, o.ForecastCategoryName, s.ForecastCategoryName stage_fc, COUNT(*) n, SUM(o.Amount) amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_stage_runs` s ON s.ApiName=o.StageName AND s._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id AND o.IsClosed=false
GROUP BY 1,2,3,4,5,6 ORDER BY 1,2,3
```
18 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Contract","Probability":"90","DefaultProbability":"90","ForecastCategoryName":"Commit","stage_fc":"Commit","n":23,"amt":"15595996"},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Creds Presentation","Probability":"25","DefaultProbability":"25","ForecastCategoryName":"Pipeline","stage_fc":"Pipeline","n":8,"amt":"6300000"},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Discovery","Probability":"10","DefaultProbability":"10","ForecastCategoryName":"Pipeline","stage_fc":"Pipeline","n":27,"amt":"9900000"},{"RecordTypeId":"012Kc000000xcSYIAY",`
### q82: Open pipeline and weighted pipeline in CAD by record type, fiscal year, forecast category
```sql
SELECT o.RecordTypeId, o.FiscalYear, o.ForecastCategoryName, COUNT(*) n, SUM(IF(o.CurrencyIsoCode='USD', o.Amount/0.737, o.Amount)) amt_cad, SUM(IF(o.CurrencyIsoCode='USD', o.Amount/0.737, o.Amount)*o.Probability/100) weighted_cad,
 SUM(IF(o.CurrencyIsoCode='USD', o.Amount/0.737, o.Amount)*s.DefaultProbability/100) weighted_default_cad, COUNTIF(o.Amount IS NULL) amt_null
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_stage_runs` s ON s.ApiName=o.StageName AND s._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id AND o.IsClosed=false GROUP BY 1,2,3 ORDER BY 1,2,3
```
11 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","FiscalYear":2025,"ForecastCategoryName":"Pipeline","n":1,"amt_cad":null,"weighted_cad":null,"weighted_default_cad":null,"amt_null":1},{"RecordTypeId":"012Kc000000xcSYIAY","FiscalYear":2026,"ForecastCategoryName":"Best Case","n":18,"amt_cad":"27947360.244233379","weighted_cad":"12658680.12211669","weighted_default_cad":"13973680.12211669","amt_null":5},{"RecordTypeId":"012Kc000000xcSYIAY","FiscalYear":2026,"ForecastCategoryName":"Commit","n":23,"amt_cad":"15595996","weighted_cad":"14036396.4","weighted_default_cad":"14036396.4","amt_null":0},{"RecordTypeId`
### q4: Stage / record type / forecast category / probability breakdown
```sql
SELECT RecordTypeId, StageName, IsClosed, IsWon, ForecastCategoryName, COUNT(*) n, SUM(Amount) amt, MIN(Probability) pmin, MAX(Probability) pmax, COUNTIF(Amount IS NULL) amt_null, COUNTIF(CurrencyIsoCode='USD') usd
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id
GROUP BY 1,2,3,4,5 ORDER BY 1,2
```
17 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Closed Lost","IsClosed":true,"IsWon":false,"ForecastCategoryName":"Omitted","n":19,"amt":"93339290","pmin":"0","pmax":"0","amt_null":0,"usd":4},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Closed Won","IsClosed":true,"IsWon":true,"ForecastCategoryName":"Closed","n":21,"amt":"15508868","pmin":"100","pmax":"100","amt_null":0,"usd":8},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Contract","IsClosed":false,"IsWon":false,"ForecastCategoryName":"Commit","n":23,"amt":"15595996","pmin":"90","pmax":"90","amt_null":0,"usd":0},{"RecordTypeId":"`
### q26: Open pipeline by close year: past due, CAD conversion, concentration, push counts
```sql
SELECT RecordTypeId, FORMAT_DATE('%Y', CloseDate) yr, COUNTIF(CloseDate < DATE '2026-09-29') past_due, COUNT(*) n, SUM(Amount) amt, SUM(IF(CurrencyIsoCode='USD', Amount/0.737, Amount)) amt_cad, MAX(Amount) max_amt, SUM(PushCount) pushes, COUNTIF(PushCount>0) pushed_opps
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND IsClosed=false GROUP BY 1,2 ORDER BY 1,2
```
6 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","yr":"2025","past_due":1,"n":1,"amt":null,"amt_cad":null,"max_amt":null,"pushes":0,"pushed_opps":0},{"RecordTypeId":"012Kc000000xcSYIAY","yr":"2026","past_due":5,"n":47,"amt":"38273196","amt_cad":"43643356.244233379","max_amt":"15000000","pushes":2,"pushed_opps":2},{"RecordTypeId":"012Kc000000xcSYIAY","yr":"2027","past_due":0,"n":33,"amt":"23050000","amt_cad":"24263297.150610584","max_amt":"5000000","pushes":28,"pushed_opps":26},{"RecordTypeId":"012Kc000000xd9cIAA","yr":"2025","past_due":1,"n":1,"amt":"42000","amt_cad":"42000","max_amt":"42000","pushes":0,`
### q43: Stage progression and regressions from OpportunityHistory by record type
```sql
WITH h AS (
 SELECT h.OpportunityId, h.StageName, h.CreatedDate, h.CloseDate,
  LAG(h.StageName) OVER (PARTITION BY h.OpportunityId ORDER BY h.CreatedDate, h.Id) prev_stage
 FROM `secnd-ml.stratis_ai.sf_opportunity_history_runs` h WHERE h._run_id=@snapshot_run_id),
r AS (SELECT *, CASE StageName WHEN 'Discovery' THEN 1 WHEN 'Creds Presentation' THEN 2 WHEN 'Proposal' THEN 3 WHEN 'Negotiation' THEN 4 WHEN 'Contract' THEN 5 WHEN 'Closed Lost' THEN 0 ELSE 6 END rk,
 CASE prev_stage WHEN 'Discovery' THEN 1 WHEN 'Creds Presentation' THEN 2 WHEN 'Proposal' THEN 3 WHEN 'Negotiation' THEN 4 WHEN 'Contract' THEN 5 WHEN 'Closed Lost' THEN 0 ELSE 6 END prk FROM h WHERE prev_stage IS NOT NULL AND prev_stage != StageName)
SELECT o.RecordTypeId,
 COUNT(*) stage_changes, COUNT(DISTINCT r.OpportunityId) opps_changed,
 COUNTIF(prk BETWEEN 1 AND 5 AND rk BETWEEN 1 AND 5 AND rk<prk) regressions,
 COUNT(DISTINCT IF(prk BETWEEN 1 AND 5 AND rk BETWEEN 1 AND 5 AND rk<prk, r.OpportunityId, NULL)) opps_regressed,
 COUNTIF(prk IN (0,6) AND rk BETWEEN 1 AND 5) reopened,
 COUNTIF(prk=6 AND rk=6) won_to_won_moves,
 COUNTIF(prk BETWEEN 1 AND 5 AND rk=6) open_to_won, COUNTIF(prk BETWEEN 1 AND 5 AND rk=0) open_to_lost, COUNTIF(prk=6 AND rk=0) won_to_lost
FROM r JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=r.OpportunityId AND o._run_id=@snapshot_run_id
GROUP BY 1
```
2 rows; first rows: `[{"RecordTypeId":"012Kc000000xd9cIAA","stage_changes":63,"opps_changed":57,"regressions":3,"opps_regressed":3,"reopened":0,"won_to_won_moves":29,"open_to_won":17,"open_to_lost":8,"won_to_lost":1},{"RecordTypeId":"012Kc000000xcSYIAY","stage_changes":78,"opps_changed":49,"regressions":7,"opps_regressed":3,"reopened":1,"won_to_won_moves":11,"open_to_won":8,"open_to_lost":14,"won_to_lost":2}]`
### q49: Close date movement from OpportunityHistory vs PushCount
```sql
WITH h AS (
 SELECT h.OpportunityId, h.CloseDate, h.PrevCloseDate, h.StageName,
  LAG(h.CloseDate) OVER (PARTITION BY h.OpportunityId ORDER BY h.CreatedDate, h.Id) lag_cd
 FROM `secnd-ml.stratis_ai.sf_opportunity_history_runs` h WHERE h._run_id=@snapshot_run_id),
c AS (SELECT OpportunityId, CloseDate, lag_cd, StageName FROM h WHERE lag_cd IS NOT NULL AND lag_cd != CloseDate),
agg AS (SELECT OpportunityId, COUNT(*) moves, COUNTIF(CloseDate>lag_cd) pushed, COUNTIF(CloseDate<lag_cd) pulled,
  COUNTIF(CloseDate>lag_cd AND DATE_TRUNC(CloseDate, MONTH)>DATE_TRUNC(lag_cd, MONTH)) pushed_month, SUM(DATE_DIFF(CloseDate, lag_cd, DAY)) net_days,
  COUNTIF(StageName IN ('Closed Won','Closed Lost','Project In Progress','Project Completion','Kick-off')) moves_on_close FROM c GROUP BY 1)
SELECT o.RecordTypeId, o.IsClosed, COUNT(*) opps, SUM(moves) moves, SUM(pushed) pushed, SUM(pulled) pulled, SUM(pushed_month) pushed_month, SUM(o.PushCount) pushcount, SUM(net_days) net_days, SUM(moves_on_close) moves_on_close
FROM agg JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=agg.OpportunityId AND o._run_id=@snapshot_run_id
GROUP BY 1,2 ORDER BY 1,2
```
4 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","IsClosed":false,"opps":29,"moves":31,"pushed":30,"pulled":1,"pushed_month":30,"pushcount":30,"net_days":5744,"moves_on_close":0},{"RecordTypeId":"012Kc000000xcSYIAY","IsClosed":true,"opps":18,"moves":21,"pushed":11,"pulled":10,"pushed_month":11,"pushcount":11,"net_days":430,"moves_on_close":7},{"RecordTypeId":"012Kc000000xd9cIAA","IsClosed":false,"opps":6,"moves":6,"pushed":3,"pulled":3,"pushed_month":3,"pushcount":3,"net_days":193,"moves_on_close":0},{"RecordTypeId":"012Kc000000xd9cIAA","IsClosed":true,"opps":9,"moves":9,"pushed":2,"pulled":7,"pushed_mon`
### q52: When and across which years open engagements were pushed
```sql
WITH h AS (
 SELECT h.OpportunityId, h.CloseDate, h.CreatedDate,
  LAG(h.CloseDate) OVER (PARTITION BY h.OpportunityId ORDER BY h.CreatedDate, h.Id) lag_cd
 FROM `secnd-ml.stratis_ai.sf_opportunity_history_runs` h WHERE h._run_id=@snapshot_run_id)
SELECT DATE(DATETIME(h.CreatedDate, 'America/New_York')) change_day, EXTRACT(YEAR FROM lag_cd) from_yr, EXTRACT(YEAR FROM h.CloseDate) to_yr, COUNT(*) n, COUNT(DISTINCT h.OpportunityId) opps
FROM h JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=h.OpportunityId AND o._run_id=@snapshot_run_id
WHERE lag_cd IS NOT NULL AND lag_cd < h.CloseDate AND o.RecordTypeId='012Kc000000xcSYIAY' AND o.IsClosed=false
GROUP BY 1,2,3 ORDER BY n DESC LIMIT 15
```
10 rows; first rows: `[{"change_day":"2026-09-21","from_yr":2026,"to_yr":2027,"n":12,"opps":12},{"change_day":"2026-09-21","from_yr":2027,"to_yr":2027,"n":4,"opps":4},{"change_day":"2026-09-21","from_yr":2026,"to_yr":2026,"n":3,"opps":3},{"change_day":"2026-09-09","from_yr":2026,"to_yr":2027,"n":3,"opps":3},{"change_day":"2026-09-10","from_yr":2026,"to_yr":2027,"n":2,"opps":2}]`
### q36: First recorded stage per opportunity: entered-closed by record type, bulk loads
```sql
WITH h AS (
 SELECT h.OpportunityId, h.StageName, h.CreatedDate, h.CloseDate, h.PrevCloseDate, h.Amount,
  ROW_NUMBER() OVER (PARTITION BY h.OpportunityId ORDER BY h.CreatedDate, h.Id) rn
 FROM `secnd-ml.stratis_ai.sf_opportunity_history_runs` h WHERE h._run_id=@snapshot_run_id),
f AS (SELECT * FROM h WHERE rn=1)
SELECT o.RecordTypeId, f.StageName first_stage, s.IsClosed first_closed, DATE(f.CreatedDate) = DATE(o.CreatedDate) same_day, COUNT(*) n,
 COUNTIF(DATE(o.CreatedDate) IN (DATE '2025-05-27', DATE '2026-07-08')) bulk, MIN(DATE(o.CreatedDate)) min_created, MAX(DATE(o.CreatedDate)) max_created
FROM f JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=f.OpportunityId AND o._run_id=@snapshot_run_id
LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_stage_runs` s ON s.ApiName=f.StageName AND s._run_id=@snapshot_run_id
GROUP BY 1,2,3,4 ORDER BY 1,2
```
15 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","first_stage":"Closed Lost","first_closed":true,"same_day":true,"n":4,"bulk":0,"min_created":"2026-07-09","max_created":"2026-07-09"},{"RecordTypeId":"012Kc000000xcSYIAY","first_stage":"Closed Won","first_closed":true,"same_day":true,"n":15,"bulk":0,"min_created":"2026-07-09","max_created":"2026-07-23"},{"RecordTypeId":"012Kc000000xcSYIAY","first_stage":"Contract","first_closed":false,"same_day":true,"n":20,"bulk":0,"min_created":"2026-09-14","max_created":"2026-09-15"},{"RecordTypeId":"012Kc000000xcSYIAY","first_stage":"Discovery","first_closed":false,"sa`
### q64: Stage creation/modification dates and descriptions (stage meaning, renames)
```sql
SELECT ApiName, MasterLabel, IsActive, SortOrder, DATE(CreatedDate) created, DATE(LastModifiedDate) modified, Description
FROM `secnd-ml.stratis_ai.sf_opportunity_stage_runs` WHERE _run_id=@snapshot_run_id ORDER BY created, SortOrder
```
18 rows; first rows: `[{"ApiName":"Qualification","MasterLabel":"Qualification","IsActive":false,"SortOrder":null,"created":"2025-01-20","modified":"2025-03-24","Description":"You've contacted the prospect and they're interested."},{"ApiName":"Needs Analysis","MasterLabel":"Needs Analysis","IsActive":false,"SortOrder":null,"created":"2025-01-20","modified":"2025-03-24","Description":"You're defining the prospect's needs."},{"ApiName":"Proposal","MasterLabel":"Proposal","IsActive":true,"SortOrder":8,"created":"2025-01-20","modified":"2026-09-17","Description":"You're developing a sales proposal for the prospect."},{`
### q67: Won stage usage over time: Closed Won vs legacy project stages
```sql
SELECT RecordTypeId, StageName, EXTRACT(YEAR FROM CloseDate) close_yr, FORMAT_DATETIME('%Y-%m', DATETIME(LastModifiedDate,'America/New_York')) >= '2026-06' mod_after_june, COUNT(*) n, MIN(DATE(DATETIME(CreatedDate,'America/New_York'))) min_created, MAX(DATE(DATETIME(CreatedDate,'America/New_York'))) max_created
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND IsWon=true
GROUP BY 1,2,3,4 ORDER BY 1,2,3
```
11 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Closed Won","close_yr":2025,"mod_after_june":true,"n":1,"min_created":"2025-11-12","max_created":"2025-11-12"},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Closed Won","close_yr":2026,"mod_after_june":true,"n":20,"min_created":"2025-10-28","max_created":"2026-07-23"},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Project Completion","close_yr":2025,"mod_after_june":false,"n":14,"min_created":"2025-05-13","max_created":"2026-01-09"},{"RecordTypeId":"012Kc000000xcSYIAY","StageName":"Project In Progress","close_yr":2025,"mod_after_june":f`
### q58: What Collaborative Forecasts facts cover (record types, categories)
```sql
SELECT o.RecordTypeId, f.ForecastCategoryName, COUNT(*) facts, COUNT(DISTINCT f.OpportunityId) opps, COUNT(DISTINCT f.ForecastingTypeId) types, COUNT(DISTINCT f.PeriodId) periods, SUM(f.TargetValue) tv
FROM `secnd-ml.stratis_ai.sf_forecasting_fact_runs` f LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=f.OpportunityId AND o._run_id=@snapshot_run_id
WHERE f._run_id=@snapshot_run_id GROUP BY 1,2
```
6 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","ForecastCategoryName":"Pipeline","facts":1,"opps":1,"types":1,"periods":1,"tv":0},{"RecordTypeId":"012Kc000000xd9cIAA","ForecastCategoryName":"Closed","facts":12,"opps":6,"types":1,"periods":4,"tv":561700},{"RecordTypeId":"012Kc000000xcSYIAY","ForecastCategoryName":"Closed","facts":14,"opps":7,"types":1,"periods":5,"tv":2911916.3600000003},{"RecordTypeId":"012Kc000000xd9cIAA","ForecastCategoryName":"Commit","facts":2,"opps":2,"types":1,"periods":1,"tv":20000},{"RecordTypeId":"012Kc000000xcSYIAY","ForecastCategoryName":"Commit","facts":1,"opps":1,"types":1`
### q59: ForecastingItem usage by type and category
```sql
SELECT ForecastingTypeId, ForecastingItemCategory, COUNT(*) n, COUNT(DISTINCT OwnerId) owners, COUNT(DISTINCT PeriodId) periods, SUM(ForecastAmount) amt, MIN(SystemModstamp) first_ts, MAX(SystemModstamp) last_ts
FROM `secnd-ml.stratis_ai.sf_forecasting_item_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1,2 ORDER BY 1,2
```
8 rows; first rows: `[{"ForecastingTypeId":"0DbKc000000gPCiKAM","ForecastingItemCategory":"BestCaseForecast","n":43,"owners":3,"periods":39,"amt":"1991808.18","first_ts":"2026-02-10T08:06:44.000Z","last_ts":"2026-09-29T13:39:22.000Z"},{"ForecastingTypeId":"0DbKc000000gPCiKAM","ForecastingItemCategory":"BestCaseOnly","n":5,"owners":2,"periods":5,"amt":"160000","first_ts":"2026-02-10T08:06:44.000Z","last_ts":"2026-07-09T01:38:07.000Z"},{"ForecastingTypeId":"0DbKc000000gPCiKAM","ForecastingItemCategory":"ClosedOnly","n":33,"owners":3,"periods":32,"amt":"1736808.18","first_ts":"2026-02-10T08:06:44.000Z","last_ts":"202`

Snapshot 20260929T163700Z.

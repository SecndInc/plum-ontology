# Findings: Revenue

I drafted four revenue metrics that pass the compile check. They agree with the accepted `gross_revenue`, but two things undercut them: the org's own revenue reports now undercount FY2026, and Media net revenue is understated.

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

## Claims

- **anomaly** (high) The PUSH KPI revenue reports (Gross Revenue - Total, PUSH Revenue - Total/Monthly) filter StageName to Financial Setup, Kick-off, Project In Progress, Project Completion, so they leave out the new Closed Won stage. For FY2025 this makes no difference: all 107 won Sales Opportunities are at those stages (13,226,393.10 CAD gross, 1,707,070.92 CAD PUSH revenue). For FY2026 the stage filter catches only 1 of 21 won projects: 348,893.2 CAD gross and 0 PUSH revenue, against 1,799,873 CAD gross and 894,924 CAD PUSH revenue by IsWon. — `q33`
- **fact** (high) Master and Sales Opportunities both carry Amount, so adding them together double counts. 24 of 62 won Master Opportunities have child Sales Opportunities (100 children). Those masters' Amount (17,517,040.45) does not equal the children's Amount (13,697,303.79), and the Sum_of_Sales_Opportunities__c rollup matches the children's sum on only 18 of the 24. — `q23`
  > Reviewer: q23's child CTE takes every Sales Opportunity with a Parent_Opportunity__c, with no IsWon filter. So '100 children' and the children's Amount of 13,697,303.79 include open and lost children, not only won projects. Both sums also add native Amount without converting currency: won master native Amount is 35,307,313.47, while q118 in CAD gives 19,948,445.47 + 15,501,008.62 = 35,449,454. The rollup may only count won children, so '18 of 24 match' could reflect the missing won filter rather than a broken rollup. Rerun with won children only and CAD conversion, or state these caveats. The double-count warning itself stands.
- **fact** (high) The won stage model changed in 2026. OpportunityStage metadata marks Financial Setup, Kick-off, Project In Progress and Project Completion as inactive but IsClosed/IsWon; the active won stage is Closed Won. In field history, moves into Project Completion run from 2025-05 to 2026-01, and moves into Closed Won only start in 2026-07. Among FY2026 won Sales Opportunities, the Closed Won stage holds 4 CAD and 16 USD records, and 1 record is at Project In Progress. — `q17`, `q66`, `q19`
- **anomaly** (high) PUSH_Revenue__c (formula: Media = Total_Media_Spend__c × Media_Fee__c, otherwise Amount − Vendor_Cost__c) is 0 on many won Media Sales Opportunities: 34 of the 67 CAD records and all 7 USD records. This happens because Media_Fee__c is blank or the monthly media spend is 0. In FY2025, 28 won Media projects with 574,745.35 in Amount have no fee % and no media spend, and 3 projects with 3,401,272.08 of media spend have a fee % that yields 0. For Agency and Creative, PUSH revenue is Amount minus vendor cost. — `q8`, `q28`
  > Reviewer: The cause sentence is incomplete. Of the 34 zero-PUSH CAD Media records in q28, 4 have Media_Fee__c filled in and nonzero media spend: 1 in FY2024 with 51,700 spend, and the 3 FY2025 records with 3,401,272.08 spend. Their fee % is presumably 0, which is neither blank fee nor zero spend. The body mentions the 3 FY2025 records but the 'this happens because' sentence does not. Also, in this data a blank fee and zero spend always occur together, so the query cannot tell which one causes the zero. Reword to three causes: blank fee with no spend (30), fee present but yielding 0 (4), and all 7 USD records blank.
- **fact** (high) The revenue budget lives in Campaigns of Type Sales, in a 3-level tree. At the top is a root campaign named '2025' (StartDate 2025-01-01 to EndDate 2025-12-31) with ExpectedRevenue 20,016,974.49. Below it are 6 middle client-level nodes: 5 have no ExpectedRevenue and 1 (New Business) holds 4,083,759, which repeats its children. At the bottom are 18 client × service-line leaf campaigns that add up to 20,016,974. Adding all non-root campaigns together double counts the New Business budget. — `q47`, `q54`
- **fact** (high) Only Master Opportunities are tagged to budget campaigns: 37 won FY2025 masters (14,381,607.02 CAD) and 4 won FY2026 masters (4,416,000 CAD). No Sales Opportunity has a CampaignId. So the campaign field AmountWonOpportunities on leaf campaigns (18,797,607.02) includes FY2026 wins against the 2025 budget. — `q44`, `q54`
- **caveat** (high) Operating_Entity__c is blank on every won Sales Opportunity closing in FY2024–FY2025, so an operating-entity breakdown only works from FY2026. Many projects were backfilled: 91 of 107 FY2025 wins were created after their CloseDate. USD appears only on Push USA FY2026 projects (16 won, 729,173 USD), but 3 Push USA wins are in CAD. — `q81`
  > Reviewer: Saying an operating-entity breakdown 'works from FY2026' is overstated. In FY2026, 1 of 21 wins (348,893.2 CAD, about 19% of FY2026 gross) still has a blank Operating_Entity__c, so an 'Unassigned' bucket is still needed. The backfill count compares DATE(CreatedDate), a UTC timestamp, with a local CloseDate, so a few records near the boundary could be misclassified. The 91/107 figure should be labelled approximate.
- **caveat** (high) Monthly_Revenue_Plan__c cannot be used as a plan. All 45 rows belong to a single Media project, several months have duplicate rows (13 for 2026-06), and many rows hold placeholder values (Media_Fees_Planned 3, Markup_Planned 1). ForecastingQuota rows run only from 2023-09-01 to 2024-02-01 and were created when the org was created, before any opportunity. — `q35`, `q38`, `q57`
  > Reviewer: 'Media_Fees_Planned 3' is a monthly SUM over 2 rows (q38 mfp), not a per-row placeholder value; only Markup_Planned is shown per row (MAX = 1). The ForecastingQuota part says the rows were 'created when the org was created, before any opportunity'. That is not evidenced: no query shows org creation or the earliest Opportunity CreatedDate. q57 only shows CreatedDate 2025-01-20. Drop that clause or add evidence. The main conclusion that neither is usable as a plan is supported.
- **fact** (high) Against the FY2025 budget of 20,016,974.49 CAD, won Master Opportunities closing in FY2025 total 19,948,445.47 CAD (42 engagements), and won Sales Opportunities (projects) total 13,226,393.10 CAD (107 projects). Budget attainment therefore depends on which record type is compared to the budget. — `q118`, `q54`

## Evidence queries

Each runs with `@snapshot_run_id` set to the snapshot below and returned the rows summarised here.

### q33: Won Sales Opportunity revenue by FY in CAD, max record, and report-stage subset
```sql
SELECT EXTRACT(YEAR FROM CloseDate) fy, COUNT(*) n, SUM(IF(CurrencyIsoCode='USD', Amount/0.737, Amount)) amt_cad, MAX(IF(CurrencyIsoCode='USD', Amount/0.737, Amount)) max_amt_cad,
SUM(IF(CurrencyIsoCode='USD', PUSH_Revenue__c/0.737, PUSH_Revenue__c)) push_cad, MAX(IF(CurrencyIsoCode='USD', PUSH_Revenue__c/0.737, PUSH_Revenue__c)) max_push_cad,
SUM(IF(StageName IN ('Kick-off','Project In Progress','Project Completion','Financial Setup'), IF(CurrencyIsoCode='USD', Amount/0.737, Amount),0)) report_stage_amt_cad,
SUM(IF(StageName IN ('Kick-off','Project In Progress','Project Completion','Financial Setup'), IF(CurrencyIsoCode='USD', PUSH_Revenue__c/0.737, PUSH_Revenue__c),0)) report_stage_push_cad,
COUNTIF(StageName IN ('Kick-off','Project In Progress','Project Completion','Financial Setup')) report_stage_n
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' AND IsWon
GROUP BY 1 ORDER BY 1
```
3 rows; first rows: `[{"fy":2024,"n":12,"amt_cad":"1565444.03","max_amt_cad":"486000","push_cad":"209936.17","max_push_cad":"85273.5","report_stage_amt_cad":"1565444.03","report_stage_push_cad":"209936.17","report_stage_n":12},{"fy":2025,"n":107,"amt_cad":"13226393.1","max_amt_cad":"3000000","push_cad":"1707070.92","max_push_cad":"174600","report_stage_amt_cad":"13226393.1","report_stage_push_cad":"1707070.92","report_stage_n":107},{"fy":2026,"n":21,"amt_cad":"1799873.118588874","max_amt_cad":"397000","push_cad":"894924.287652646","max_push_cad":"397000","report_stage_amt_cad":"348893.2","report_stage_push_cad":"0`
### q23: Master vs child Sales opportunity amounts; double-count risk
```sql
WITH s AS (SELECT Parent_Opportunity__c pid, COUNT(*) n_child, SUM(Amount) child_amt, SUM(PUSH_Revenue__c) child_push FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' AND Parent_Opportunity__c IS NOT NULL GROUP BY 1)
SELECT m.IsWon, COUNT(*) masters, COUNTIF(s.pid IS NOT NULL) with_children, SUM(s.n_child) children, SUM(m.Amount) master_amt, SUM(IF(s.pid IS NOT NULL, m.Amount, 0)) master_amt_with_children, SUM(s.child_amt) child_amt, SUM(m.Sum_of_Sales_Opportunities__c) rollup_amt,
COUNTIF(s.pid IS NOT NULL AND ABS(IFNULL(m.Sum_of_Sales_Opportunities__c,0)-s.child_amt)<1) rollup_matches
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` m LEFT JOIN s ON s.pid=m.Id
WHERE m._run_id=@snapshot_run_id AND m.RecordTypeId='012Kc000000xcSYIAY' GROUP BY 1
```
2 rows; first rows: `[{"IsWon":false,"masters":100,"with_children":22,"children":65,"master_amt":"154662486","master_amt_with_children":"12165496","child_amt":"6884901","rollup_amt":"6369414","rollup_matches":11},{"IsWon":true,"masters":62,"with_children":24,"children":100,"master_amt":"35307313.47","master_amt_with_children":"17517040.45","child_amt":"13697303.79","rollup_amt":"12704510.65","rollup_matches":18}]`
### q17: Stage metadata: which stages are closed/won
```sql
SELECT MasterLabel, ApiName, IsActive, IsClosed, IsWon, DefaultProbability, ForecastCategoryName, SortOrder FROM `secnd-ml.stratis_ai.sf_opportunity_stage_runs` WHERE _run_id = @snapshot_run_id ORDER BY SortOrder
```
18 rows; first rows: `[{"MasterLabel":"Qualification","ApiName":"Qualification","IsActive":false,"IsClosed":false,"IsWon":false,"DefaultProbability":"10","ForecastCategoryName":"Pipeline","SortOrder":null},{"MasterLabel":"Needs Analysis","ApiName":"Needs Analysis","IsActive":false,"IsClosed":false,"IsWon":false,"DefaultProbability":"35","ForecastCategoryName":"Pipeline","SortOrder":null},{"MasterLabel":"Financial Setup","ApiName":"Financial Setup","IsActive":false,"IsClosed":true,"IsWon":true,"DefaultProbability":"100","ForecastCategoryName":"Closed","SortOrder":null},{"MasterLabel":"Kick-off","ApiName":"Kick-off",`
### q66: Stage transitions over time: when Closed Won replaced project stages
```sql
SELECT OldValue, NewValue, COUNT(*) n, FORMAT_TIMESTAMP('%Y-%m', MIN(CreatedDate)) mn, FORMAT_TIMESTAMP('%Y-%m', MAX(CreatedDate)) mx FROM `secnd-ml.stratis_ai.sf_opportunity_field_history_runs` WHERE _run_id=@snapshot_run_id AND Field='StageName' GROUP BY 1,2 ORDER BY n DESC LIMIT 30
```
30 rows; first rows: `[{"OldValue":"Project In Progress","NewValue":"Project Completion","n":33,"mn":"2025-05","mx":"2026-01"},{"OldValue":"Discovery","NewValue":"Proposal","n":17,"mn":"2025-07","mx":"2026-09"},{"OldValue":"Proposal","NewValue":"Closed Lost","n":11,"mn":"2025-08","mx":"2026-09"},{"OldValue":"Discovery","NewValue":"Creds Presentation","n":11,"mn":"2026-06","mx":"2026-09"},{"OldValue":"Proposal","NewValue":"Closed Won","n":8,"mn":"2026-07","mx":"2026-09"}]`
### q19: Won Sales Opportunities by fiscal year, stage and currency
```sql
SELECT EXTRACT(YEAR FROM CloseDate) fy, StageName, CurrencyIsoCode, COUNT(*) n, SUM(Amount) amt, SUM(PUSH_Revenue__c) push_rev, MIN(CloseDate) mn, MAX(CloseDate) mx
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id = @snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' AND IsWon
GROUP BY 1,2,3 ORDER BY 1,2,3
```
8 rows; first rows: `[{"fy":2024,"StageName":"Project Completion","CurrencyIsoCode":"CAD","n":9,"amt":"1449654.03","push_rev":"120247.43","mn":"2024-09-25","mx":"2024-12-23"},{"fy":2024,"StageName":"Project In Progress","CurrencyIsoCode":"CAD","n":3,"amt":"115790","push_rev":"89688.74","mn":"2024-12-17","mx":"2024-12-28"},{"fy":2025,"StageName":"Kick-off","CurrencyIsoCode":"CAD","n":2,"amt":"12250","push_rev":"12250","mn":"2025-10-31","mx":"2025-10-31"},{"fy":2025,"StageName":"Project Completion","CurrencyIsoCode":"CAD","n":93,"amt":"12317945.9","push_rev":"1613402.3","mn":"2025-01-01","mx":"2025-12-31"},{"fy":202`
### q8: Won Sales Opportunities: PUSH revenue behavior by Type and currency
```sql
SELECT Type, CurrencyIsoCode, COUNT(*) n, SUM(Amount) amt, SUM(PUSH_Revenue__c) push_rev, COUNTIF(PUSH_Revenue__c=0) push_zero, COUNTIF(Media_Fee__c IS NOT NULL) has_fee, COUNTIF(Vendor_Cost__c IS NOT NULL) has_vendor, SUM(Fees_Amount__c) fees, COUNTIF(Fees_Amount__c IS NULL) fees_null, SUM(Total_Media_Spend__c) media, COUNTIF(Amount IS NULL) amt_null
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id = @snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' AND IsWon
GROUP BY 1,2 ORDER BY 1,2
```
6 rows; first rows: `[{"Type":"Agency","CurrencyIsoCode":"CAD","n":14,"amt":"238330","push_rev":"220690.69","push_zero":0,"has_fee":0,"has_vendor":3,"fees":"108735","fees_null":6,"media":"0","amt_null":0},{"Type":"Agency","CurrencyIsoCode":"USD","n":4,"amt":"80961","push_rev":"80961","push_zero":0,"has_fee":0,"has_vendor":0,"fees":"79760","fees_null":0,"media":"0","amt_null":0},{"Type":"Creative","CurrencyIsoCode":"CAD","n":43,"amt":"1077639.9","push_rev":"1016922.4","push_zero":0,"has_fee":0,"has_vendor":11,"fees":"917569","fees_null":28,"media":"0","amt_null":0},{"Type":"Creative","CurrencyIsoCode":"USD","n":5,"`
### q28: Why PUSH Revenue is zero on many won Media projects
```sql
SELECT CurrencyIsoCode, (PUSH_Revenue__c=0) push_zero, Media_Fee__c IS NULL fee_null, Total_Media_Spend__c=0 media_zero, EXTRACT(YEAR FROM CloseDate) fy, COUNT(*) n, SUM(Amount) amt, SUM(Fees_Amount__c) fees, SUM(Total_Media_Spend__c) media, SUM(PUSH_Revenue__c) push, COUNTIF(ABS(IFNULL(Fees_Amount__c,0)-Amount)<1) fees_eq_amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' AND IsWon AND Type='Media'
GROUP BY 1,2,3,4,5 ORDER BY 5,1,2,3,4
```
8 rows; first rows: `[{"CurrencyIsoCode":"CAD","push_zero":false,"fee_null":false,"media_zero":false,"fy":2024,"n":7,"amt":"1167704.03","fees":"1176329.03","media":"1012838.98","push":"121682.67","fees_eq_amt":6},{"CurrencyIsoCode":"CAD","push_zero":true,"fee_null":false,"media_zero":false,"fy":2024,"n":1,"amt":"290400","fees":null,"media":"51700","push":"0","fees_eq_amt":0},{"CurrencyIsoCode":"CAD","push_zero":true,"fee_null":true,"media_zero":true,"fy":2024,"n":1,"amt":"14000","fees":"14000","media":"0","push":"0","fees_eq_amt":1},{"CurrencyIsoCode":"CAD","push_zero":false,"fee_null":false,"media_zero":false,"fy`
### q47: Budget campaign structure (names are budget lines, not people)
```sql
SELECT c.Id, c.Name, c.ParentId, c.Status, c.ExpectedRevenue, c.BudgetedCost, c.AmountWonOpportunities, c.NumberOfWonOpportunities, c.StartDate, c.EndDate, c.CreatedDate
FROM `secnd-ml.stratis_ai.sf_campaign_runs` c WHERE c._run_id=@snapshot_run_id ORDER BY c.ParentId NULLS FIRST, c.ExpectedRevenue DESC
```
25 rows; first rows: `[{"Id":"701JQ000014Wf8VYAS","Name":"2025","ParentId":null,"Status":"In Progress","ExpectedRevenue":"20016974.49","BudgetedCost":null,"AmountWonOpportunities":"0","NumberOfWonOpportunities":0,"StartDate":"2025-01-01","EndDate":"2025-12-31","CreatedDate":"2025-12-17T21:48:33.000Z"},{"Id":"701JQ000014c8t7YAA","Name":"2025 - New Business","ParentId":"701JQ000014Wf8VYAS","Status":"In Progress","ExpectedRevenue":"4083759","BudgetedCost":null,"AmountWonOpportunities":"0","NumberOfWonOpportunities":0,"StartDate":null,"EndDate":null,"CreatedDate":"2025-12-19T00:33:40.000Z"},{"Id":"701JQ000014bm84YAA","`
### q54: Budget hierarchy: root vs middle vs leaf ExpectedRevenue totals
```sql
WITH kids AS (SELECT DISTINCT ParentId FROM `secnd-ml.stratis_ai.sf_campaign_runs` WHERE _run_id=@snapshot_run_id AND ParentId IS NOT NULL)
SELECT CASE WHEN c.ParentId IS NULL THEN 'root' WHEN k.ParentId IS NULL THEN 'leaf' ELSE 'middle' END lvl, COUNT(*) n, SUM(c.ExpectedRevenue) exp_rev, COUNTIF(c.ExpectedRevenue IS NULL) exp_null, SUM(c.AmountWonOpportunities) won_amt
FROM `secnd-ml.stratis_ai.sf_campaign_runs` c LEFT JOIN kids k ON k.ParentId=c.Id WHERE c._run_id=@snapshot_run_id GROUP BY 1
```
3 rows; first rows: `[{"lvl":"root","n":1,"exp_rev":"20016974.49","exp_null":0,"won_amt":"0"},{"lvl":"middle","n":6,"exp_rev":"4083759","exp_null":5,"won_amt":"0"},{"lvl":"leaf","n":18,"exp_rev":"20016974","exp_null":0,"won_amt":"18797607.02"}]`
### q44: Which opportunities are tagged to budget campaigns
```sql
SELECT o.RecordTypeId, o.IsWon, EXTRACT(YEAR FROM o.CloseDate) fy, COUNT(*) n, COUNT(DISTINCT o.CampaignId) camps, SUM(IF(o.CurrencyIsoCode='USD',o.Amount/0.737,o.Amount)) amt_cad, SUM(IF(o.CurrencyIsoCode='USD',o.PUSH_Revenue__c/0.737,o.PUSH_Revenue__c)) push_cad
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o WHERE o._run_id=@snapshot_run_id AND o.CampaignId IS NOT NULL GROUP BY 1,2,3 ORDER BY 1,2,3
```
4 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","IsWon":false,"fy":2025,"n":8,"camps":3,"amt_cad":"64160000","push_cad":"150000"},{"RecordTypeId":"012Kc000000xcSYIAY","IsWon":false,"fy":2026,"n":6,"camps":2,"amt_cad":"28075000","push_cad":"75000"},{"RecordTypeId":"012Kc000000xcSYIAY","IsWon":true,"fy":2025,"n":37,"camps":13,"amt_cad":"14381607.02","push_cad":"1363245.2"},{"RecordTypeId":"012Kc000000xcSYIAY","IsWon":true,"fy":2026,"n":4,"camps":2,"amt_cad":"4416000","push_cad":"0"}]`
### q81: Sales opps by operating entity/currency/FY; future-dated and backdated wins
```sql
SELECT Operating_Entity__c, CurrencyIsoCode, EXTRACT(YEAR FROM CloseDate) fy, COUNT(*) n, COUNTIF(IsWon) won, COUNTIF(IsWon AND CloseDate > DATE '2026-09-29') won_future, COUNTIF(IsWon AND DATE(CreatedDate) > CloseDate) won_created_after_close, SUM(IF(IsWon, Amount, 0)) won_amt_native
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND RecordTypeId='012Kc000000xd9cIAA' GROUP BY 1,2,3 ORDER BY 3,1,2
```
9 rows; first rows: `[{"Operating_Entity__c":null,"CurrencyIsoCode":"CAD","fy":2024,"n":12,"won":12,"won_future":0,"won_created_after_close":12,"won_amt_native":"1565444.03"},{"Operating_Entity__c":null,"CurrencyIsoCode":"CAD","fy":2025,"n":111,"won":107,"won_future":0,"won_created_after_close":91,"won_amt_native":"13226393.1"},{"Operating_Entity__c":"Push Canada","CurrencyIsoCode":"CAD","fy":2025,"n":2,"won":0,"won_future":0,"won_created_after_close":0,"won_amt_native":"0"},{"Operating_Entity__c":null,"CurrencyIsoCode":"CAD","fy":2026,"n":3,"won":1,"won_future":0,"won_created_after_close":1,"won_amt_native":"3488`
### q35: Monthly revenue plan coverage: which projects and months
```sql
SELECT o.RecordTypeId, o.StageName, o.Type, o.CurrencyIsoCode, COUNT(DISTINCT p.Project__c) projects, COUNT(*) plan_rows, MIN(p.Month__c) mn, MAX(p.Month__c) mx, SUM(p.Total_Planned__c) planned, SUM(p.Total_Actual__c) actual, SUM(p.Media_Fees_Planned__c) mf_plan, SUM(p.Media_Fees_Actual__c) mf_act, COUNTIF(p.Media_Fees_Actual__c IS NOT NULL) act_rows, COUNTIF(EXTRACT(DAY FROM p.Month__c)!=1) not_first
FROM `secnd-ml.stratis_ai.sf_monthly_revenue_plan_runs` p LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=p.Project__c AND o._run_id=@snapshot_run_id
WHERE p._run_id=@snapshot_run_id GROUP BY 1,2,3,4
```
1 row; first rows: `[{"RecordTypeId":"012Kc000000xd9cIAA","StageName":"Project Completion","Type":"Media","CurrencyIsoCode":"CAD","projects":1,"plan_rows":45,"mn":"2026-01-01","mx":"2027-04-01","planned":"121691.49","actual":"105391","mf_plan":"100549","mf_act":"87100","act_rows":7,"not_first":0}]`
### q38: Plan rows per month: duplicates / test data
```sql
SELECT Month__c, COUNT(*) n, SUM(Total_Planned__c) planned, SUM(Total_Actual__c) actual, SUM(Media_Fees_Planned__c) mfp, MAX(Markup_Planned__c) mk, COUNTIF(Notes__c IS NOT NULL) notes, MIN(CreatedDate) c1, MAX(CreatedDate) c2
FROM `secnd-ml.stratis_ai.sf_monthly_revenue_plan_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1 ORDER BY 1
```
16 rows; first rows: `[{"Month__c":"2026-01-01","n":2,"planned":"16214","actual":"16214","mfp":"13400","mk":"21","notes":2,"c1":"2026-04-27T02:45:33.000Z","c2":"2026-04-27T03:32:51.000Z"},{"Month__c":"2026-02-01","n":1,"planned":"16214","actual":"16214","mfp":"13400","mk":"21","notes":1,"c1":"2026-04-27T03:09:23.000Z","c2":"2026-04-27T03:09:23.000Z"},{"Month__c":"2026-03-01","n":1,"planned":"16214","actual":"16214","mfp":"13400","mk":"21","notes":1,"c1":"2026-04-27T03:12:05.000Z","c2":"2026-04-27T03:12:05.000Z"},{"Month__c":"2026-04-01","n":1,"planned":"24321","actual":"24321","mfp":"20100","mk":"21","notes":1,"c1"`
### q57: Forecasting quotas as revenue targets
```sql
SELECT q.StartDate, q.QuotaAmount, q.CurrencyIsoCode, q.ForecastingTypeId, q.PeriodId, q.QuotaQuantity, q.IsQuantity, q.CreatedDate FROM `secnd-ml.stratis_ai.sf_forecasting_quota_runs` q WHERE q._run_id=@snapshot_run_id ORDER BY q.StartDate
```
6 rows; first rows: `[{"StartDate":"2023-09-01","QuotaAmount":"40000","CurrencyIsoCode":"CAD","ForecastingTypeId":"0DbKc000000gPCiKAM","PeriodId":"026Kc0000019wPZIAY","QuotaQuantity":0,"IsQuantity":false,"CreatedDate":"2025-01-20T05:42:53.000Z"},{"StartDate":"2023-10-01","QuotaAmount":"30000","CurrencyIsoCode":"CAD","ForecastingTypeId":"0DbKc000000gPCiKAM","PeriodId":"026Kc0000019wPYIAY","QuotaQuantity":0,"IsQuantity":false,"CreatedDate":"2025-01-20T05:42:53.000Z"},{"StartDate":"2023-11-01","QuotaAmount":"50000","CurrencyIsoCode":"CAD","ForecastingTypeId":"0DbKc000000gPCiKAM","PeriodId":"026Kc0000019wPeIAI","Quota`
### q118: Won amount by record type and FY vs budget-tagged
```sql
SELECT RecordTypeId, EXTRACT(YEAR FROM CloseDate) fy, COUNT(*) n, SUM(IF(CurrencyIsoCode='USD',Amount/0.737,Amount)) amt_cad, COUNTIF(CampaignId IS NOT NULL) tagged, SUM(IF(CampaignId IS NOT NULL, IF(CurrencyIsoCode='USD',Amount/0.737,Amount),0)) tagged_amt_cad
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` WHERE _run_id=@snapshot_run_id AND IsWon AND EXTRACT(YEAR FROM CloseDate) IN (2025,2026) GROUP BY 1,2 ORDER BY 1,2
```
4 rows; first rows: `[{"RecordTypeId":"012Kc000000xcSYIAY","fy":2025,"n":42,"amt_cad":"19948445.47","tagged":37,"tagged_amt_cad":"14381607.02"},{"RecordTypeId":"012Kc000000xcSYIAY","fy":2026,"n":20,"amt_cad":"15501008.616010855","tagged":4,"tagged_amt_cad":"4416000"},{"RecordTypeId":"012Kc000000xd9cIAA","fy":2025,"n":107,"amt_cad":"13226393.1","tagged":0,"tagged_amt_cad":"0"},{"RecordTypeId":"012Kc000000xd9cIAA","fy":2026,"n":21,"amt_cad":"1799873.118588874","tagged":0,"tagged_amt_cad":"0"}]`

Snapshot 20260929T163700Z.

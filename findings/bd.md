# Findings: Business development

Business-development topic, snapshot 20260929T163700Z (15 queries used).

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

## Claims

- **fact** (high) Win rate differs sharply by Business_Type__c. FY2025 engagements: Exisiting 39 won of 41 decided, New 3 of 6, New - RFP 0 of 5. FY2026 to date: Exisiting 10 of 13, New 9 of 12, New - RFP 0 of 3, Organic Growth 1 of 1. The picklist value is spelled "Exisiting" in the data. — `q34`
  > Reviewer: The counts match q34, but "differs sharply" only holds for FY2025 and for New - RFP. In FY2026, Exisiting won 10 of 13 (77%) and New won 9 of 12 (75%), which is nearly the same. The FY2025 Exisiting rate of 39/41 is mostly backfilled wins: 39 of the 42 FY2025 wins were created already at a won stage (q32), so the gap partly reflects how data was loaded, not selling performance. Several cells are tiny (Organic Growth 1 of 1, New - RFP 0 of 3). Say which differences hold in which year and add the backfill and small-sample caveats.
- **anomaly** (high) Engagement Amount is dominated by a few large lost bids, so an amount-weighted win rate would be misleading. One FY2026 Closed Lost New - RFP media engagement of 27000000 CAD is 60.3% of all FY2026 decided engagement value; in FY2025 the largest single decided engagement (23000000, Closed Lost) is 27.3% of 84108445 CAD. Count-based win rate is the defensible measure. — `q50`, `q53`
- **caveat** (high) Operating_Entity__c is effectively populated only from FY2026. For engagements closing FY2025 it is blank on 50 of 53 (41 of 42 won); for FY2026 it is blank on 5 of 76 and on none of the 20 won. Projects: blank on 111 of 113 in FY2025 and all 12 in FY2024. Splitting by operating entity before FY2026 therefore puts almost everything in "blank". Currency does not identify the entity: Push USA records exist in both CAD and USD. — `q56`, `q18`
- **fact** (high) Wins are concentrated in a handful of clients in FY2025: 42 won engagements came from 9 distinct accounts, with one account holding 13 wins. In FY2026 the 20 wins span 19 accounts (max 2 per account). — `q45`
- **definition** (high) Engagements are Master_Opportunity records (162); projects are Sales_Opportunity records. 165 projects point via Parent_Opportunity__c to 46 distinct engagements, 6 projects point to another project, and 26 projects have no parent. 160 of the 165 master-parented projects share the engagement's account. Engagement Amount is not the sum of its projects: of 24 won engagements with projects, their Amount sums to 17517040.45 vs 13697303.79 on their children, and 38 won engagements have no project at all. Counting both record types together double-counts the same work. — `q15`, `q22`
- **caveat** (high) Engagement win rate is inflated by backfilled wins. Among engagements closing in FY2025, 34 won ones were first recorded already at Project In Progress and 5 already at Project Completion; FY2025 engagements that entered the pipeline open split 3 won, 8 lost. In FY2026, 15 wins were entered directly as Closed Won; engagements that entered open split 5 won, 5 lost (47 still open). — `q32`
  > Reviewer: The won counts are right, but the claim leaves out backfilled losses. In FY2025, 2 losses were first recorded at Project In Progress. In FY2026, 4 engagements were created already Closed Lost (q32). Backfilling is not wins-only: in FY2026 the records created already closed split 15 won / 4 lost (79%), against 5 / 5 for those that entered the pipeline open. That still shows inflation, but include the backfilled losses. Also, a record created directly at Closed Won in FY2026 may be a real deal entered late rather than a historical backfill.
- **caveat** (medium) Business_Type__c mostly agrees with account history, but not always: engagements tagged New on accounts that had already won earlier number 7 (1 won) with blank Account.Type plus 1 (1 won) on a Customer account; engagements tagged Exisiting on accounts that never won number 9 plus 1. Account.Type is blank for most accounts and is not a usable new/existing flag. — `q39`
  > Reviewer: The counts match q39, but the history test has flaws that should be stated. (1) first_win is built from all record types, so an engagement's own child project closing before the engagement's CloseDate makes the account look like it "won earlier". Some of the 7+1 "New on accounts that won earlier" may be this artefact. (2) "Account never won" only covers history inside this CRM, which starts around 2024. Exisiting engagements on never-won accounts can be clients from before the CRM, so they are not necessarily mis-tagged. (3) The Account.Type statement is counted per engagement, not per account; either re-count by account or say "blank on most engagements' accounts".
- **fact** (high) Every opportunity created in the 2026-07-08 bulk load carries an operating entity (Push Canada, Push USA or Stratis), and the load mixes open and already-closed records; for example 8 Push USA engagements were loaded already won and 4 already lost, and 16 Push USA projects were loaded already won. No duplicate engagements were found: 0 engagements mirror a project on account + name + close date, and only 1 name pair repeats within projects. — `q62`, `q72`
  > Reviewer: The bulk-load breakdown matches q62, and it reconciles with q56 (36 engagements, 40 projects). "No duplicate engagements were found" is overstated, though. q72 only catches exact matches on account plus trimmed, lower-cased name (plus the exact same CloseDate for the cross-record-type check). Bulk loads usually create near-duplicates with slightly different names or dates, which this test cannot see. Restate as "no exact-name duplicates" and note that no fuzzy check was run on the bulk-loaded records against earlier ones. Also, the 2026-07-08 date assumes America/New_York is the org's time zone.
- **anomaly** (high) "Won" by IsWon covers stage Closed Won plus the delivery stages Kick-off, Project In Progress and Project Completion. The BD won-count KPI reports (this FY and past FY) filter only on Kick-off, Project In Progress, Project Completion and leave out Closed Won. For engagements closing FY2025 that gives 41 vs 42 by IsWon; for FY2026 it gives 0 vs 20, because every FY2026 engagement win sits in stage Closed Won. The stage-list reports therefore undercount wins from FY2026 onward. — `q9`
  > Reviewer: The IsWon-vs-stage-list counts (41 vs 42, 0 vs 20) are correct per q9. The central claim, that the BD KPI reports filter only on Kick-off, Project In Progress and Project Completion, is not supported by any attached evidence: no report metadata was queried. q9 just counts records under an assumed stage list. Attach the report filter definitions, or mark the report filter as unverified. The reports' date field and any other filters also need confirming before saying they "undercount from FY2026 onward".

## Evidence queries

Each runs with `@snapshot_run_id` set to the snapshot below and returned the rows summarised here.

### q34: Engagement win/decided by business type and FY
```sql
SELECT EXTRACT(YEAR FROM o.CloseDate) fy, IFNULL(o.Business_Type__c,'(blank)') bt,
 COUNTIF(o.IsClosed) decided, COUNTIF(o.IsWon) won, COUNTIF(NOT o.IsClosed) open_n, COUNT(DISTINCT o.AccountId) accounts
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
WHERE o._run_id = @snapshot_run_id AND rt.DeveloperName='Master_Opportunity'
GROUP BY 1,2 ORDER BY 1,2
```
11 rows; first rows: `[{"fy":2025,"bt":"(blank)","decided":0,"won":0,"open_n":1,"accounts":1},{"fy":2025,"bt":"Exisiting","decided":41,"won":39,"open_n":0,"accounts":7},{"fy":2025,"bt":"New","decided":6,"won":3,"open_n":0,"accounts":6},{"fy":2025,"bt":"New - RFP","decided":5,"won":0,"open_n":0,"accounts":5},{"fy":2026,"bt":"(blank)","decided":0,"won":0,"open_n":1,"accounts":1}]`
### q50: Engagement amount by FY/closed in CAD, top-record concentration, zero-probability open records
```sql
WITH m AS (
 SELECT o.Id, EXTRACT(YEAR FROM o.CloseDate) fy, o.IsClosed, o.IsWon, o.Probability, o.StageName, o.Type,
  o.Amount / CASE o.CurrencyIsoCode WHEN 'USD' THEN 0.737 ELSE 1 END amt_cad
 FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id AND rt.DeveloperName='Master_Opportunity')
SELECT fy, IsClosed, COUNT(*) n, COUNTIF(Probability=0) prob0, ROUND(SUM(amt_cad),0) amt_cad, ROUND(MAX(amt_cad),0) max_amt,
 ROUND(MAX(amt_cad)/SUM(amt_cad)*100,1) top_share_pct
FROM m GROUP BY 1,2 ORDER BY 1,2
```
5 rows; first rows: `[{"fy":2025,"IsClosed":false,"n":1,"prob0":0,"amt_cad":null,"max_amt":null,"top_share_pct":null},{"fy":2025,"IsClosed":true,"n":52,"prob0":10,"amt_cad":84108445,"max_amt":23000000,"top_share_pct":27.3},{"fy":2026,"IsClosed":false,"n":47,"prob0":3,"amt_cad":43643356,"max_amt":20352782,"top_share_pct":46.6},{"fy":2026,"IsClosed":true,"n":29,"prob0":9,"amt_cad":44744279,"max_amt":27000000,"top_share_pct":60.3},{"fy":2027,"IsClosed":false,"n":33,"prob0":0,"amt_cad":24263297,"max_amt":5000000,"top_share_pct":20.6}]`
### q53: Largest engagements and open engagements with 0 probability
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id),
kids AS (SELECT Parent_Opportunity__c pid, COUNT(*) nk, SUM(Amount) kid_amt FROM o WHERE rt='Sales_Opportunity' GROUP BY 1)
SELECT m.Id, EXTRACT(YEAR FROM m.CloseDate) fy, m.StageName, m.IsWon, m.Probability, m.Type, m.Business_Type__c, m.Operating_Entity__c, m.Amount, m.CurrencyIsoCode, k.nk, k.kid_amt
FROM o m LEFT JOIN kids k ON k.pid=m.Id
WHERE m.rt='Master_Opportunity' AND (m.Amount >= 5000000 OR (NOT m.IsClosed AND m.Probability=0))
ORDER BY m.Amount DESC
```
13 rows; first rows: `[{"Id":"006Kc000005Sat3IAC","fy":2026,"StageName":"Closed Lost","IsWon":false,"Probability":"0","Type":"Media","Business_Type__c":"New - RFP","Operating_Entity__c":"Push Canada","Amount":"27000000","CurrencyIsoCode":"CAD","nk":null,"kid_amt":null},{"Id":"006Kc000005SAiqIAG","fy":2025,"StageName":"Closed Lost","IsWon":false,"Probability":"0","Type":"Media","Business_Type__c":"New","Operating_Entity__c":null,"Amount":"23000000","CurrencyIsoCode":"CAD","nk":null,"kid_amt":null},{"Id":"006Kc000005SaIcIAK","fy":2025,"StageName":"Closed Lost","IsWon":false,"Probability":"0","Type":"Media","Business_`
### q56: Operating entity fill by record type and close FY; bulk load of 2026-07-08
```sql
SELECT rt.DeveloperName rt, EXTRACT(YEAR FROM o.CloseDate) fy, COUNT(*) n, COUNTIF(o.Operating_Entity__c IS NULL) oe_blank,
 COUNTIF(o.IsWon) won, COUNTIF(o.IsWon AND o.Operating_Entity__c IS NULL) won_oe_blank,
 COUNTIF(DATE(o.CreatedDate,'America/New_York')='2026-07-08') bulk_0708
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
WHERE o._run_id = @snapshot_run_id
GROUP BY 1,2 ORDER BY 1,2
```
7 rows; first rows: `[{"rt":"Master_Opportunity","fy":2025,"n":53,"oe_blank":50,"won":42,"won_oe_blank":41,"bulk_0708":0},{"rt":"Master_Opportunity","fy":2026,"n":76,"oe_blank":5,"won":20,"won_oe_blank":0,"bulk_0708":33},{"rt":"Master_Opportunity","fy":2027,"n":33,"oe_blank":0,"won":0,"won_oe_blank":0,"bulk_0708":3},{"rt":"Sales_Opportunity","fy":2024,"n":12,"oe_blank":12,"won":12,"won_oe_blank":12,"bulk_0708":0},{"rt":"Sales_Opportunity","fy":2025,"n":113,"oe_blank":111,"won":107,"won_oe_blank":107,"bulk_0708":0}]`
### q18: Fill of operating entity, business type, service line, currency by record type
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id)
SELECT rt, IFNULL(Operating_Entity__c,'(blank)') oe, IFNULL(Business_Type__c,'(blank)') bt, IFNULL(Type,'(blank)') typ, CurrencyIsoCode cur, COUNT(*) n
FROM o GROUP BY 1,2,3,4,5 ORDER BY 1,2,3,4,5
```
51 rows; first rows: `[{"rt":"Master_Opportunity","oe":"(blank)","bt":"(blank)","typ":"(blank)","cur":"CAD","n":2},{"rt":"Master_Opportunity","oe":"(blank)","bt":"Exisiting","typ":"Agency","cur":"CAD","n":5},{"rt":"Master_Opportunity","oe":"(blank)","bt":"Exisiting","typ":"Creative","cur":"CAD","n":12},{"rt":"Master_Opportunity","oe":"(blank)","bt":"Exisiting","typ":"Media","cur":"CAD","n":24},{"rt":"Master_Opportunity","oe":"(blank)","bt":"New","typ":"Media","cur":"CAD","n":5}]`
### q45: Distinct clients won per FY and concentration of wins in one client; probability of lost
```sql
WITH m AS (
 SELECT o.AccountId, EXTRACT(YEAR FROM o.CloseDate) fy, o.IsWon, o.IsClosed, o.Probability, o.StageName
 FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id AND rt.DeveloperName='Master_Opportunity'),
acc AS (SELECT fy, AccountId, COUNTIF(IsWon) w FROM m GROUP BY 1,2)
SELECT fy, COUNTIF(w>0) clients_won, MAX(w) max_wins_one_client, SUM(w) wins,
 (SELECT COUNTIF(Probability>0) FROM m WHERE m.fy=acc.fy AND StageName='Closed Lost') lost_prob_gt0,
 (SELECT COUNT(*) FROM m WHERE m.fy=acc.fy AND Probability=0) prob0
FROM acc GROUP BY fy ORDER BY fy
```
3 rows; first rows: `[{"fy":2025,"clients_won":9,"max_wins_one_client":13,"wins":42,"lost_prob_gt0":0,"prob0":10},{"fy":2026,"clients_won":19,"max_wins_one_client":2,"wins":20,"lost_prob_gt0":0,"prob0":12},{"fy":2027,"clients_won":0,"max_wins_one_client":0,"wins":0,"lost_prob_gt0":0,"prob0":0}]`
### q15: Parent/child structure between projects and engagements
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id)
SELECT c.rt child_rt, p.rt parent_rt, COUNT(*) n, COUNT(DISTINCT c.Parent_Opportunity__c) parents,
 COUNTIF(c.AccountId = p.AccountId) same_account,
 COUNTIF(c.Type = p.Type) same_type,
 COUNTIF(c.Business_Type__c = p.Business_Type__c) same_bt
FROM o c LEFT JOIN o p ON p.Id = c.Parent_Opportunity__c
GROUP BY 1,2
```
4 rows; first rows: `[{"child_rt":"Sales_Opportunity","parent_rt":null,"n":26,"parents":0,"same_account":0,"same_type":0,"same_bt":0},{"child_rt":"Master_Opportunity","parent_rt":null,"n":162,"parents":0,"same_account":0,"same_type":0,"same_bt":0},{"child_rt":"Sales_Opportunity","parent_rt":"Master_Opportunity","n":165,"parents":46,"same_account":160,"same_type":152,"same_bt":147},{"child_rt":"Sales_Opportunity","parent_rt":"Sales_Opportunity","n":6,"parents":3,"same_account":6,"same_type":5,"same_bt":5}]`
### q22: Does engagement amount equal sum of child projects?
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id),
kids AS (SELECT Parent_Opportunity__c pid, COUNT(*) nk, SUM(Amount) kid_amt FROM o WHERE rt='Sales_Opportunity' GROUP BY 1)
SELECT p.IsWon, (k.pid IS NOT NULL) has_kids, COUNT(*) masters, SUM(p.Amount) master_amt, SUM(k.kid_amt) kid_amt, SUM(p.Sum_of_Sales_Opportunities__c) rollup_amt,
 COUNTIF(ABS(p.Amount - IFNULL(k.kid_amt,0)) < 1) amt_eq_kids
FROM o p LEFT JOIN kids k ON k.pid = p.Id WHERE p.rt='Master_Opportunity'
GROUP BY 1,2 ORDER BY 1,2
```
4 rows; first rows: `[{"IsWon":false,"has_kids":false,"masters":78,"master_amt":"142496990","kid_amt":null,"rollup_amt":null,"amt_eq_kids":12},{"IsWon":false,"has_kids":true,"masters":22,"master_amt":"12165496","kid_amt":"6884901","rollup_amt":"6369414","amt_eq_kids":4},{"IsWon":true,"has_kids":false,"masters":38,"master_amt":"17790273.02","kid_amt":null,"rollup_amt":null,"amt_eq_kids":0},{"IsWon":true,"has_kids":true,"masters":24,"master_amt":"17517040.45","kid_amt":"13697303.79","rollup_amt":"12704510.65","amt_eq_kids":4}]`
### q32: Engagements entered already closed, by close FY — bias in win rate
```sql
WITH o AS (
 SELECT o.Id, o.IsWon, o.IsClosed, EXTRACT(YEAR FROM o.CloseDate) fy, DATE(o.CreatedDate,'America/New_York') cd, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id),
first_stage AS (
 SELECT OpportunityId, ARRAY_AGG(StageName ORDER BY CreatedDate LIMIT 1)[OFFSET(0)] fs
 FROM `secnd-ml.stratis_ai.sf_opportunity_history_runs` WHERE _run_id = @snapshot_run_id GROUP BY 1)
SELECT o.rt, o.fy, CASE WHEN f.fs IS NULL THEN 'no history' WHEN f.fs IN ('Closed Won','Closed Lost','Project Completion','Project In Progress','Kick-off') THEN CONCAT('entered closed: ',f.fs) ELSE 'entered open' END entry,
 COUNTIF(o.IsWon) won, COUNTIF(o.IsClosed AND NOT o.IsWon) lost, COUNTIF(NOT o.IsClosed) open_n
FROM o LEFT JOIN first_stage f ON f.OpportunityId=o.Id
WHERE o.rt='Master_Opportunity'
GROUP BY 1,2,3 ORDER BY 1,2,3
```
7 rows; first rows: `[{"rt":"Master_Opportunity","fy":2025,"entry":"entered closed: Project Completion","won":5,"lost":0,"open_n":0},{"rt":"Master_Opportunity","fy":2025,"entry":"entered closed: Project In Progress","won":34,"lost":2,"open_n":0},{"rt":"Master_Opportunity","fy":2025,"entry":"entered open","won":3,"lost":8,"open_n":1},{"rt":"Master_Opportunity","fy":2026,"entry":"entered closed: Closed Lost","won":0,"lost":4,"open_n":0},{"rt":"Master_Opportunity","fy":2026,"entry":"entered closed: Closed Won","won":15,"lost":0,"open_n":0}]`
### q39: Is Business_Type consistent with account win history and Account.Type?
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id),
first_win AS (SELECT AccountId, MIN(CloseDate) fw FROM o WHERE IsWon GROUP BY 1)
SELECT m.Business_Type__c bt, a.Type acct_type,
 CASE WHEN f.fw IS NULL THEN 'account never won' WHEN f.fw < m.CloseDate THEN 'account won earlier' WHEN f.fw = m.CloseDate THEN 'first win same day' ELSE 'first win later' END hist,
 COUNT(*) n, COUNTIF(m.IsWon) won
FROM o m LEFT JOIN first_win f ON f.AccountId=m.AccountId
LEFT JOIN `secnd-ml.stratis_ai.sf_account_runs` a ON a.Id=m.AccountId AND a._run_id=@snapshot_run_id
WHERE m.rt='Master_Opportunity'
GROUP BY 1,2,3 ORDER BY 1,2,3
```
19 rows; first rows: `[{"bt":null,"acct_type":null,"hist":"account never won","n":2,"won":0},{"bt":"Exisiting","acct_type":null,"hist":"account never won","n":9,"won":0},{"bt":"Exisiting","acct_type":null,"hist":"account won earlier","n":38,"won":23},{"bt":"Exisiting","acct_type":null,"hist":"first win same day","n":6,"won":6},{"bt":"Exisiting","acct_type":"Customer","hist":"account never won","n":1,"won":0}]`
### q62: What the 2026-07-08 bulk load contains
```sql
SELECT rt.DeveloperName rt, IFNULL(o.Operating_Entity__c,'(blank)') oe, o.IsClosed, o.IsWon, COUNT(*) n, COUNT(DISTINCT o.AccountId) accts
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
WHERE o._run_id = @snapshot_run_id AND DATE(o.CreatedDate,'America/New_York')='2026-07-08'
GROUP BY 1,2,3,4 ORDER BY 1,2,3,4
```
11 rows; first rows: `[{"rt":"Master_Opportunity","oe":"Push Canada","IsClosed":false,"IsWon":false,"n":11,"accts":10},{"rt":"Master_Opportunity","oe":"Push Canada","IsClosed":true,"IsWon":true,"n":3,"accts":3},{"rt":"Master_Opportunity","oe":"Push USA","IsClosed":false,"IsWon":false,"n":6,"accts":5},{"rt":"Master_Opportunity","oe":"Push USA","IsClosed":true,"IsWon":false,"n":4,"accts":3},{"rt":"Master_Opportunity","oe":"Push USA","IsClosed":true,"IsWon":true,"n":8,"accts":7}]`
### q72: Duplicate engagements within and across record types
```sql
WITH o AS (
 SELECT o.*, rt.DeveloperName rt FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
 JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
 WHERE o._run_id = @snapshot_run_id),
g AS (SELECT rt, AccountId, LOWER(TRIM(Name)) nm, COUNT(*) n, COUNTIF(IsWon) w FROM o GROUP BY 1,2,3 HAVING COUNT(*)>1),
x AS (SELECT a.Id FROM o a JOIN o b ON a.rt='Master_Opportunity' AND b.rt='Sales_Opportunity' AND a.AccountId=b.AccountId AND LOWER(TRIM(a.Name))=LOWER(TRIM(b.Name)) AND a.CloseDate=b.CloseDate)
SELECT 'same name within rt' k, rt, COUNT(*) grp_n, SUM(n) recs, SUM(w) won FROM g GROUP BY rt
UNION ALL SELECT 'master mirrors sales (acct+name+closedate)', 'cross', COUNT(DISTINCT Id), NULL, NULL FROM x
```
2 rows; first rows: `[{"k":"same name within rt","rt":"Sales_Opportunity","grp_n":1,"recs":2,"won":2},{"k":"master mirrors sales (acct+name+closedate)","rt":"cross","grp_n":0,"recs":null,"won":null}]`
### q9: Won/decided per fiscal year and record type, IsWon vs report stage list
```sql
SELECT EXTRACT(YEAR FROM o.CloseDate) fy, rt.DeveloperName rt,
 COUNT(*) total,
 COUNTIF(o.IsClosed) decided, COUNTIF(o.IsWon) won,
 COUNTIF(o.StageName IN ('Kick-off','Project In Progress','Project Completion')) won_stage_list,
 COUNTIF(o.StageName='Closed Won') closed_won_stage,
 COUNTIF(o.StageName='Closed Lost') lost,
 COUNTIF(NOT o.IsClosed) open_n,
 ROUND(SUM(o.Amount),2) amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
WHERE o._run_id = @snapshot_run_id
GROUP BY 1,2 ORDER BY 2,1
```
7 rows; first rows: `[{"fy":2025,"rt":"Master_Opportunity","total":53,"decided":52,"won":42,"won_stage_list":41,"closed_won_stage":1,"lost":10,"open_n":1,"amt":"84108445.47"},{"fy":2026,"rt":"Master_Opportunity","total":76,"decided":29,"won":20,"won_stage_list":0,"closed_won_stage":20,"lost":9,"open_n":47,"amt":"82811354"},{"fy":2027,"rt":"Master_Opportunity","total":33,"decided":0,"won":0,"won_stage_list":0,"closed_won_stage":0,"lost":0,"open_n":33,"amt":"23050000"},{"fy":2024,"rt":"Sales_Opportunity","total":12,"decided":12,"won":12,"won_stage_list":12,"closed_won_stage":0,"lost":0,"open_n":0,"amt":"1565444.03"}`
### q5: Stage x record type x IsWon/IsClosed distribution
```sql
SELECT rt.DeveloperName, o.StageName, o.IsClosed, o.IsWon, COUNT(*) n, SUM(CASE WHEN o.Amount IS NULL THEN 1 ELSE 0 END) no_amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id = o.RecordTypeId AND rt._run_id = @snapshot_run_id
WHERE o._run_id = @snapshot_run_id
GROUP BY 1,2,3,4 ORDER BY 1,2
```
16 rows; first rows: `[{"DeveloperName":"Master_Opportunity","StageName":"Closed Lost","IsClosed":true,"IsWon":false,"n":19,"no_amt":0},{"DeveloperName":"Master_Opportunity","StageName":"Closed Won","IsClosed":true,"IsWon":true,"n":21,"no_amt":0},{"DeveloperName":"Master_Opportunity","StageName":"Contract","IsClosed":false,"IsWon":false,"n":23,"no_amt":0},{"DeveloperName":"Master_Opportunity","StageName":"Creds Presentation","IsClosed":false,"IsWon":false,"n":8,"no_amt":1},{"DeveloperName":"Master_Opportunity","StageName":"Discovery","IsClosed":false,"IsWon":false,"n":27,"no_amt":1}]`

Snapshot 20260929T163700Z.

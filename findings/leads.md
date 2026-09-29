# Findings: Leads and campaigns

I used 17 of the 35 queries. The main finding: campaigns in this org are budget lines, not marketing campaigns. And until September 2026, leads were mostly a way to enter a deal, not a real funnel. Six metrics passed validation. Three open questions go to reviewers, each with the default I used.

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

## Claims

- **fact** (high) Lead Status and IsConverted are fully aligned: all 46 converted leads have Status 'Qualified' and every Qualified lead is converted; no unconverted lead is Qualified. Open statuses are New Lead (96), New (30), Working (2), Nurturing (1), Internal Debrief (1). Of the 46 converted leads, 38 carry a ConvertedOpportunityId and 42 a ConvertedAccountId, and all 46 have a ConvertedDate. — `q2`
- **anomaly** (high) 100 leads were created in a single insert at 2026-09-01T21:32:44Z by one user: all LeadSource 'Referral - Team', all CurrencyIsoCode USD, 100 distinct companies (large US brands). 96 remain Status 'New Lead' (the only leads with that status value) and 4 were converted between 2026-09-02 and 2026-09-09 (3 with an opportunity). This one list import is 100 of the 143 leads created in 2026 Q3. — `q6`, `q10`, `q48`
- **fact** (high) Before the September 2026 import, leads were used mainly as a way to create opportunities rather than as a nurtured funnel: 33 of the 41 converted leads outside the bulk import and org-creation seed were converted on the same day they were created, and the lead cohorts of 2025 Q3 (11 of 11), 2025 Q4 (5 of 5), 2026 Q1 (1 of 1) and 2026 Q2 (3 of 3) are all converted. Cohort conversion rates by created date are therefore near 100% until 2026 Q3 (19 of 143). — `q10`, `q48`
  > Reviewer: 'Near 100% until 2026 Q3' is overstated. The 2025 Q1 cohort is 3 of 8 (37.5%, dragged down by the 5 unconverted seed leads) and 2025 Q2 is 4 of 5. Only 2025 Q3 through 2026 Q2 are 100%. Also, the '33 of 41 same-day' figure is not a pre-import figure: the organic cohort's ConvertedDate runs to 2026-09-17, and about 15 organic 2026 Q3 leads were converted after the import. At least 18 of the 26 organic conversions before Q3 2026 must be same-day, but the exact pre-import number was not measured. Either restrict the query to CreatedDate < 2026-09-01 or drop the 'before the September 2026 import' framing. Also note that 7 of the 41 created no opportunity.
- **anomaly** (high) Six leads were created at the org creation timestamp 2025-01-20T05:42:53Z (Salesforce seed/sample leads, Status New/Working/Nurturing/Qualified; 1 converted), and 6 leads have test company names ('Test', 'Test Company', 'vtg test'), 5 of them converted. These are not real prospects. — `q10`, `q51`
- **anomaly** (high) Converted-opportunity amounts are dominated by a few large lost engagements: the 11 lost Master Opportunities from lead conversion total 92,000,000 CAD, and single converted opportunities of 27,000,000 and 23,000,000 exist. Leads converted in 2025 Q3 carry 68,617,700 of opportunity amount across 10 opportunities. 'Sum of Opportunity Amount' in the Leads Converted reports is therefore a Master-engagement estimate, mostly lost, not revenue. — `q16`, `q21`, `q55`
- **fact** (high) Campaigns in this org are not marketing campaigns but a 2025 revenue budget tree: 1 root campaign '2025', 6 client-level children (5 named clients plus 'New Business'), and 18 service-line leaves (Creative / Media / Special Projects per client). All are Type 'Sales', CAD. There are no campaign members: NumberOfLeads, NumberOfContacts and NumberOfResponses are 0 on every campaign. — `q25`, `q42`
  > Reviewer: The hierarchy (1 root, 6 client nodes, 18 leaves) is supported by q25/q42. But 'all Type Sales, CAD' and 'NumberOfLeads/NumberOfContacts/NumberOfResponses are 0 on every campaign' are not shown: q25 does not select Type, CurrencyIsoCode or any member-count field. Run a query that shows these, or remove them. This matters because campaign_revenue_budget filters on Type = 'Sales'.
- **fact** (high) Lead conversion creates mostly engagements: the converted opportunities present in the snapshot are Master_Opportunity (11 lost, 3 won, 17 open) and a handful of Sales_Opportunity (3 lost, 1 won, 1 open). 2 converted leads point to opportunities no longer in the snapshot and 4 converted leads have no ConvertedAccountId. 39 converted accounts were created on the conversion date (new accounts); only 3 existed before conversion. — `q16`, `q21`
- **fact** (high) Leads are a minor path into the pipeline: 144 Master Opportunities and 194 Sales Opportunities have a blank Opportunity.LeadSource, and every Master Opportunity with a LeadSource value (Referral - Team 8, Referral - Partner 5, Website 4, Advertisement 1) came from lead conversion. LeadSource therefore cannot attribute the pipeline at large; only 13 blank-source Master Opportunities came from leads. — `q63`
- **anomaly** (high) Campaign ExpectedRevenue (budget) and Net_Revenue__c are entered at more than one level of the hierarchy, so summing all campaigns double counts: the root holds 20,016,974.49 of ExpectedRevenue and 4,201,683.64 of Net_Revenue__c, the 18 service-line leaves sum to 20,016,974 and 4,201,683.64, and the client level adds another 4,083,759 (the 'New Business' node repeating its leaves). Only the 18 leaves carry opportunity rollups (41 won, 18,797,607.02 won value). — `q25`, `q42`
- **fact** (high) Only Master Opportunities are tagged with a campaign (41 won totalling 18,797,607.02, 11 lost, 3 open, all CAD), matching the campaign rollup AmountWonOpportunities total. The won value is not limited to 2025 closes: 37 won in 2025 (14,381,607.02) and 4 won in 2026 (4,416,000). The 'New Business - Media' leaf's 96,620,000 AmountAllOpportunities is driven by lost engagements (8 lost 2025 closes total 64,160,000; 3 lost 2026 closes total 28,000,000). — `q31`, `q46`, `q25`
  > Reviewer: The loss figures come from q46, which covers all campaign-tagged engagements, not the 'New Business - Media' leaf. The 8 lost 2025 closes (64,160,000) span 3 campaigns. The Choice Hotels Creative and Media leaves each hold 150,000 and 10,000 of non-won value, so New Business - Media's share of 2025 losses is about 64,000,000. Its total non-won value is 92,000,000 (96,620,000 minus 4,620,000 won). Restate the numbers per leaf, or say they are totals across all tagged engagements. The rest (Master-only tagging, 41 won = 18,797,607.02, 37/4 split by close year) is supported.
- **caveat** (high) Campaign tagging covers most but not all won engagements: 37 of 42 Master Opportunities won in 2025 are tagged to a budget campaign (14,381,607.02 of 19,948,445.47 in Amount), but only 4 of 20 won in 2026 (4,416,000 of 15,358,868). There is no 2026 budget campaign tree, so budget-vs-actual via campaigns is only meaningful for 2025. — `q136`, `q25`
  > Reviewer: The counts are right. But the Amount totals (19,948,445.47 and 15,358,868) sum native amounts across currencies: q31 shows 8 untagged won Master Opportunities are USD, while all tagged ones are non-USD. So the tagged-share-by-amount comparison mixes CAD and USD. Convert to CAD, or report share by count only. Also, 'most' holds only for 2025 (37/42); 2026 is 4/20.

## Evidence queries

Each runs with `@snapshot_run_id` set to the snapshot below and returned the rows summarised here.

### q2: Lead status vs conversion flags and bulk load
```sql
SELECT Status, IsConverted, COUNT(*) n, COUNTIF(ConvertedOpportunityId IS NOT NULL) with_opp, COUNTIF(ConvertedAccountId IS NOT NULL) with_acct, COUNTIF(ConvertedDate IS NOT NULL) with_cdate, COUNTIF(DATE(CreatedDate,'America/New_York')='2026-09-01') bulk_0901
FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1,2 ORDER BY 1,2
```
6 rows; first rows: `[{"Status":"Internal Debrief","IsConverted":false,"n":1,"with_opp":0,"with_acct":0,"with_cdate":0,"bulk_0901":0},{"Status":"New","IsConverted":false,"n":30,"with_opp":0,"with_acct":0,"with_cdate":0,"bulk_0901":0},{"Status":"New Lead","IsConverted":false,"n":96,"with_opp":0,"with_acct":0,"with_cdate":0,"bulk_0901":96},{"Status":"Nurturing","IsConverted":false,"n":1,"with_opp":0,"with_acct":0,"with_cdate":0,"bulk_0901":0},{"Status":"Qualified","IsConverted":true,"n":46,"with_opp":38,"with_acct":42,"with_cdate":46,"bulk_0901":4}]`
### q6: Characterize bulk-loaded leads vs organic ones
```sql
SELECT DATE(CreatedDate,'America/New_York')='2026-09-01' bulk, CreatedById, OwnerId LIKE '00G%' queue_owned, LeadSource, CurrencyIsoCode, COUNT(*) n, MIN(CreatedDate) mn, MAX(CreatedDate) mx, COUNT(DISTINCT Company) companies
FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1,2,3,4,5 ORDER BY n DESC
```
23 rows; first rows: `[{"bulk":true,"CreatedById":"005JQ00000KwHo9YAF","queue_owned":false,"LeadSource":"Referral - Team","CurrencyIsoCode":"USD","n":100,"mn":"2026-09-01T21:32:44.000Z","mx":"2026-09-01T21:32:44.000Z","companies":100},{"bulk":false,"CreatedById":"005JQ00000HifP5YAJ","queue_owned":false,"LeadSource":"Referral - Partner","CurrencyIsoCode":"CAD","n":18,"mn":"2026-09-14T17:54:08.000Z","mx":"2026-09-17T16:04:46.000Z","companies":17},{"bulk":false,"CreatedById":"005Kc000001VbnmIAC","queue_owned":false,"LeadSource":null,"CurrencyIsoCode":"CAD","n":14,"mn":"2025-07-16T15:29:11.000Z","mx":"2026-07-05T05:59:`
### q10: Cohorts of leads: bulk load, org seed, organic; conversion timing
```sql
SELECT CASE WHEN CreatedDate='2026-09-01T21:32:44Z' THEN 'bulk_2026_09_01' WHEN CreatedDate='2025-01-20T05:42:53Z' THEN 'org_creation_seed' ELSE 'organic' END cohort,
 Status, IsConverted, COUNT(*) n, MIN(ConvertedDate) min_cd, MAX(ConvertedDate) max_cd, COUNTIF(ConvertedDate < DATE(CreatedDate,'America/New_York')) conv_before_created,
 COUNTIF(ConvertedDate = DATE(CreatedDate,'America/New_York')) conv_same_day, COUNTIF(ConvertedOpportunityId IS NOT NULL) with_opp, STRING_AGG(DISTINCT Company LIMIT 6) sample_companies
FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1,2,3 ORDER BY 1,2
```
9 rows; first rows: `[{"cohort":"bulk_2026_09_01","Status":"New Lead","IsConverted":false,"n":96,"min_cd":null,"max_cd":null,"conv_before_created":0,"conv_same_day":0,"with_opp":0,"sample_companies":"AbbVie,Activision Blizzard,Adobe,ADP,Airbnb,Albertsons"},{"cohort":"bulk_2026_09_01","Status":"Qualified","IsConverted":true,"n":4,"min_cd":"2026-09-02","max_cd":"2026-09-09","conv_before_created":0,"conv_same_day":0,"with_opp":3,"sample_companies":"Church & Dwight,Constellation Brands,Disney,Target"},{"cohort":"org_creation_seed","Status":"New","IsConverted":false,"n":2,"min_cd":null,"max_cd":null,"conv_before_create`
### q48: Leads created by fiscal quarter with cohort conversion, bulk and test records, TZ sensitivity
```sql
SELECT EXTRACT(YEAR FROM DATE(CreatedDate,'America/New_York')) yr, EXTRACT(QUARTER FROM DATE(CreatedDate,'America/New_York')) q,
 COUNT(*) created, COUNTIF(IsConverted) converted_of_cohort, COUNTIF(CreatedDate='2026-09-01T21:32:44Z') bulk, COUNTIF(LOWER(Company) LIKE '%test%' OR LOWER(Company) LIKE '%sample%') testish,
 COUNTIF(DATE(CreatedDate,'America/New_York') != DATE(CreatedDate)) tz_shift
FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id GROUP BY 1,2 ORDER BY 1,2
```
7 rows; first rows: `[{"yr":2025,"q":1,"created":8,"converted_of_cohort":3,"bulk":0,"testish":1,"tz_shift":0},{"yr":2025,"q":2,"created":5,"converted_of_cohort":4,"bulk":0,"testish":3,"tz_shift":0},{"yr":2025,"q":3,"created":11,"converted_of_cohort":11,"bulk":0,"testish":0,"tz_shift":0},{"yr":2025,"q":4,"created":5,"converted_of_cohort":5,"bulk":0,"testish":0,"tz_shift":0},{"yr":2026,"q":1,"created":1,"converted_of_cohort":1,"bulk":0,"testish":0,"tz_shift":0}]`
### q51: Inspect test-like lead records (company names only)
```sql
SELECT Company, Status, IsConverted, LeadSource, DATE(CreatedDate,'America/New_York') cdate, ConvertedOpportunityId IS NOT NULL has_opp
FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id AND (LOWER(Company) LIKE '%test%' OR LOWER(Company) LIKE '%sample%')
```
6 rows; first rows: `[{"Company":"Test Company","Status":"Qualified","IsConverted":true,"LeadSource":null,"cdate":"2026-04-13","has_opp":true},{"Company":"Test","Status":"Qualified","IsConverted":true,"LeadSource":null,"cdate":"2026-07-08","has_opp":true},{"Company":"vtg test","Status":"Qualified","IsConverted":true,"LeadSource":null,"cdate":"2025-03-27","has_opp":false},{"Company":"Test","Status":"Qualified","IsConverted":true,"LeadSource":null,"cdate":"2025-04-14","has_opp":false},{"Company":"Test","Status":"Internal Debrief","IsConverted":false,"LeadSource":null,"cdate":"2025-05-26","has_opp":false}]`
### q16: Record type and outcome of opportunities created by lead conversion
```sql
SELECT rt.DeveloperName rt, o.IsClosed, o.IsWon, COUNT(*) n, SUM(o.Amount) amt, COUNTIF(o.CurrencyIsoCode='USD') usd,
 COUNTIF(DATE(o.CreatedDate,'America/New_York')=l.ConvertedDate) opp_created_on_convert,
 COUNTIF(a.CreatedDate < l.CreatedDate) acct_preexisting, COUNT(DISTINCT l.ConvertedOpportunityId) distinct_opps
FROM `secnd-ml.stratis_ai.sf_lead_runs` l
JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=l.ConvertedOpportunityId AND o._run_id=@snapshot_run_id
LEFT JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id=o.RecordTypeId AND rt._run_id=@snapshot_run_id
LEFT JOIN `secnd-ml.stratis_ai.sf_account_runs` a ON a.Id=l.ConvertedAccountId AND a._run_id=@snapshot_run_id
WHERE l._run_id=@snapshot_run_id GROUP BY 1,2,3
```
6 rows; first rows: `[{"rt":"Master_Opportunity","IsClosed":true,"IsWon":false,"n":11,"amt":"92000000","usd":0,"opp_created_on_convert":11,"acct_preexisting":0,"distinct_opps":11},{"rt":"Master_Opportunity","IsClosed":true,"IsWon":true,"n":3,"amt":"4420000","usd":0,"opp_created_on_convert":3,"acct_preexisting":0,"distinct_opps":3},{"rt":"Sales_Opportunity","IsClosed":true,"IsWon":true,"n":1,"amt":"397000","usd":0,"opp_created_on_convert":1,"acct_preexisting":0,"distinct_opps":1},{"rt":"Master_Opportunity","IsClosed":false,"IsWon":false,"n":17,"amt":"18175000","usd":3,"opp_created_on_convert":16,"acct_preexisting":`
### q21: Referential integrity of converted leads to Account/Contact/Opportunity
```sql
SELECT COUNT(*) converted, COUNTIF(l.ConvertedAccountId IS NULL) no_acct_id, COUNTIF(l.ConvertedAccountId IS NOT NULL AND a.Id IS NULL) acct_missing_in_snapshot,
 COUNTIF(a.Id IS NOT NULL AND DATE(a.CreatedDate,'America/New_York') < l.ConvertedDate) acct_existing_before_convert,
 COUNTIF(a.Id IS NOT NULL AND DATE(a.CreatedDate,'America/New_York') = l.ConvertedDate) acct_created_on_convert,
 COUNTIF(a.Id IS NOT NULL AND DATE(a.CreatedDate,'America/New_York') > l.ConvertedDate) acct_created_after,
 COUNTIF(l.ConvertedContactId IS NOT NULL AND c.Id IS NULL) contact_missing,
 COUNTIF(l.ConvertedOpportunityId IS NOT NULL AND o.Id IS NULL) opp_missing,
 COUNT(DISTINCT l.ConvertedAccountId) distinct_accts,
 MAX(o.Amount) max_opp_amt
FROM `secnd-ml.stratis_ai.sf_lead_runs` l
LEFT JOIN `secnd-ml.stratis_ai.sf_account_runs` a ON a.Id=l.ConvertedAccountId AND a._run_id=@snapshot_run_id
LEFT JOIN `secnd-ml.stratis_ai.sf_contact_runs` c ON c.Id=l.ConvertedContactId AND c._run_id=@snapshot_run_id
LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=l.ConvertedOpportunityId AND o._run_id=@snapshot_run_id
WHERE l._run_id=@snapshot_run_id AND l.IsConverted
```
1 row; first rows: `[{"converted":46,"no_acct_id":4,"acct_missing_in_snapshot":0,"acct_existing_before_convert":3,"acct_created_on_convert":39,"acct_created_after":0,"contact_missing":0,"opp_missing":2,"distinct_accts":41,"max_opp_amt":"27000000"}]`
### q55: Converted leads by converted fiscal quarter with converted opportunity amount
```sql
SELECT EXTRACT(YEAR FROM l.ConvertedDate) cyr, EXTRACT(QUARTER FROM l.ConvertedDate) cq, COUNT(*) converted, COUNTIF(l.ConvertedOpportunityId IS NOT NULL) with_opp_id, COUNTIF(o.Id IS NOT NULL) opp_present,
 SUM(o.Amount) opp_amt_native, SUM(CASE WHEN o.CurrencyIsoCode='USD' THEN o.Amount/0.737 ELSE o.Amount END) opp_amt_cad, MAX(o.Amount) max_amt,
 COUNTIF(LOWER(l.Company) LIKE '%test%') test_leads, COUNTIF(l.LeadSource IS NULL) no_source
FROM `secnd-ml.stratis_ai.sf_lead_runs` l LEFT JOIN `secnd-ml.stratis_ai.sf_opportunity_runs` o ON o.Id=l.ConvertedOpportunityId AND o._run_id=@snapshot_run_id
WHERE l._run_id=@snapshot_run_id AND l.IsConverted GROUP BY 1,2 ORDER BY 1,2
```
7 rows; first rows: `[{"cyr":2025,"cq":1,"converted":2,"with_opp_id":0,"opp_present":0,"opp_amt_native":null,"opp_amt_cad":null,"max_amt":null,"test_leads":1,"no_source":2},{"cyr":2025,"cq":2,"converted":4,"with_opp_id":1,"opp_present":1,"opp_amt_native":"23000000","opp_amt_cad":"23000000","max_amt":"23000000","test_leads":2,"no_source":3},{"cyr":2025,"cq":3,"converted":10,"with_opp_id":10,"opp_present":10,"opp_amt_native":"68617700","opp_amt_cad":"68617700","max_amt":"27000000","test_leads":0,"no_source":3},{"cyr":2025,"cq":4,"converted":7,"with_opp_id":7,"opp_present":7,"opp_amt_native":"4920000","opp_amt_cad":"`
### q25: Campaign hierarchy and rollup fields
```sql
SELECT c.Id, c.ParentId, p.Name parent_name, c.Name, c.Status, c.ExpectedRevenue, c.Net_Revenue__c, c.NumberOfOpportunities, c.NumberOfWonOpportunities, c.AmountAllOpportunities, c.AmountWonOpportunities,
 (SELECT COUNT(*) FROM `secnd-ml.stratis_ai.sf_campaign_runs` k WHERE k._run_id=@snapshot_run_id AND k.ParentId=c.Id) n_children
FROM `secnd-ml.stratis_ai.sf_campaign_runs` c
LEFT JOIN `secnd-ml.stratis_ai.sf_campaign_runs` p ON p.Id=c.ParentId AND p._run_id=@snapshot_run_id
WHERE c._run_id=@snapshot_run_id ORDER BY parent_name, c.Name
```
25 rows; first rows: `[{"Id":"701JQ000014Wf8VYAS","ParentId":null,"parent_name":null,"Name":"2025","Status":"In Progress","ExpectedRevenue":"20016974.49","Net_Revenue__c":"4201683.64","NumberOfOpportunities":0,"NumberOfWonOpportunities":0,"AmountAllOpportunities":"0","AmountWonOpportunities":"0","n_children":6},{"Id":"701JQ000014cFHlYAM","ParentId":"701JQ000014Wf8VYAS","parent_name":"2025","Name":"2025 - Choice Hotels Canada","Status":"In Progress","ExpectedRevenue":null,"Net_Revenue__c":null,"NumberOfOpportunities":0,"NumberOfWonOpportunities":0,"AmountAllOpportunities":"0","AmountWonOpportunities":"0","n_children`
### q42: Campaign hierarchy levels: show budget double counting across levels
```sql
WITH c AS (
 SELECT c.*, CASE WHEN c.ParentId IS NULL THEN 'L0_root' WHEN p.ParentId IS NULL THEN 'L1_client' ELSE 'L2_service_line' END lvl
 FROM `secnd-ml.stratis_ai.sf_campaign_runs` c LEFT JOIN `secnd-ml.stratis_ai.sf_campaign_runs` p ON p.Id=c.ParentId AND p._run_id=@snapshot_run_id
 WHERE c._run_id=@snapshot_run_id)
SELECT lvl, COUNT(*) n, SUM(ExpectedRevenue) exp_rev, SUM(Net_Revenue__c) net_rev, SUM(AmountWonOpportunities) won_amt, SUM(AmountAllOpportunities) all_amt, SUM(NumberOfOpportunities) n_opps, SUM(NumberOfWonOpportunities) n_won, COUNTIF(ExpectedRevenue IS NULL) exp_null, COUNTIF(Net_Revenue__c IS NULL) net_null
FROM c GROUP BY lvl ORDER BY lvl
```
3 rows; first rows: `[{"lvl":"L0_root","n":1,"exp_rev":"20016974.49","net_rev":"4201683.64","won_amt":"0","all_amt":"0","n_opps":0,"n_won":0,"exp_null":0,"net_null":0},{"lvl":"L1_client","n":6,"exp_rev":"4083759","net_rev":null,"won_amt":"0","all_amt":"0","n_opps":0,"n_won":0,"exp_null":5,"net_null":6},{"lvl":"L2_service_line","n":18,"exp_rev":"20016974","net_rev":"4201683.64","won_amt":"18797607.02","all_amt":"111032607.02","n_opps":55,"n_won":41,"exp_null":0,"net_null":0}]`
### q63: Opportunity LeadSource fill by record type and link to converted leads
```sql
SELECT rt.DeveloperName rt, o.LeadSource, COUNT(*) n, COUNTIF(o.IsWon) won,
 COUNTIF(o.Id IN (SELECT ConvertedOpportunityId FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id AND ConvertedOpportunityId IS NOT NULL)) from_lead
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o LEFT JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id=o.RecordTypeId AND rt._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id GROUP BY 1,2 ORDER BY 1,3 DESC
```
8 rows; first rows: `[{"rt":"Master_Opportunity","LeadSource":null,"n":144,"won":59,"from_lead":13},{"rt":"Master_Opportunity","LeadSource":"Referral - Team","n":8,"won":2,"from_lead":8},{"rt":"Master_Opportunity","LeadSource":"Referral - Partner","n":5,"won":1,"from_lead":5},{"rt":"Master_Opportunity","LeadSource":"Website","n":4,"won":0,"from_lead":4},{"rt":"Master_Opportunity","LeadSource":"Advertisement","n":1,"won":0,"from_lead":1}]`
### q31: Which opportunities are tagged with a campaign, by record type and outcome
```sql
SELECT o.CampaignId IS NOT NULL has_campaign, rt.DeveloperName rt, o.IsWon, o.IsClosed, COUNT(*) n, SUM(o.Amount) amt, EXTRACT(YEAR FROM MIN(o.CloseDate)) min_yr, EXTRACT(YEAR FROM MAX(o.CloseDate)) max_yr, COUNTIF(o.CurrencyIsoCode='USD') usd
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
LEFT JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id=o.RecordTypeId AND rt._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id GROUP BY 1,2,3,4 ORDER BY 1,2,3,4
```
9 rows; first rows: `[{"has_campaign":false,"rt":"Master_Opportunity","IsWon":false,"IsClosed":false,"n":78,"amt":"61248196","min_yr":2025,"max_yr":2027,"usd":9},{"has_campaign":false,"rt":"Master_Opportunity","IsWon":false,"IsClosed":true,"n":8,"amt":"1179290","min_yr":2025,"max_yr":2026,"usd":4},{"has_campaign":false,"rt":"Master_Opportunity","IsWon":true,"IsClosed":true,"n":21,"amt":"16509706.45","min_yr":2025,"max_yr":2026,"usd":8},{"has_campaign":false,"rt":"Sales_Opportunity","IsWon":false,"IsClosed":false,"n":46,"amt":"2215286","min_yr":2025,"max_yr":2027,"usd":14},{"has_campaign":false,"rt":"Sales_Opportun`
### q46: Campaign-tagged engagements by close year and outcome; overlap with converted leads
```sql
SELECT EXTRACT(YEAR FROM o.CloseDate) close_yr, o.IsWon, o.IsClosed, COUNT(*) n, SUM(o.Amount) amt, MAX(o.Amount) max_amt, COUNT(DISTINCT o.CampaignId) n_campaigns,
 COUNTIF(o.Id IN (SELECT ConvertedOpportunityId FROM `secnd-ml.stratis_ai.sf_lead_runs` WHERE _run_id=@snapshot_run_id AND ConvertedOpportunityId IS NOT NULL)) from_lead
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o
WHERE o._run_id=@snapshot_run_id AND o.CampaignId IS NOT NULL GROUP BY 1,2,3 ORDER BY 1,2,3
```
5 rows; first rows: `[{"close_yr":2025,"IsWon":false,"IsClosed":true,"n":8,"amt":"64160000","max_amt":"23000000","n_campaigns":3,"from_lead":6},{"close_yr":2025,"IsWon":true,"IsClosed":true,"n":37,"amt":"14381607.02","max_amt":"3480000","n_campaigns":13,"from_lead":1},{"close_yr":2026,"IsWon":false,"IsClosed":false,"n":3,"amt":"75000","max_amt":"75000","n_campaigns":2,"from_lead":0},{"close_yr":2026,"IsWon":false,"IsClosed":true,"n":3,"amt":"28000000","max_amt":"27000000","n_campaigns":1,"from_lead":3},{"close_yr":2026,"IsWon":true,"IsClosed":true,"n":4,"amt":"4416000","max_amt":"3000000","n_campaigns":2,"from_lea`
### q136: Share of won engagements per year tagged to a budget campaign
```sql
SELECT EXTRACT(YEAR FROM o.CloseDate) yr, COUNT(*) won_master, COUNTIF(o.CampaignId IS NOT NULL) tagged, SUM(o.Amount) amt, SUM(IF(o.CampaignId IS NOT NULL,o.Amount,0)) tagged_amt
FROM `secnd-ml.stratis_ai.sf_opportunity_runs` o JOIN `secnd-ml.stratis_ai.sf_record_type_runs` rt ON rt.Id=o.RecordTypeId AND rt._run_id=@snapshot_run_id
WHERE o._run_id=@snapshot_run_id AND rt.DeveloperName='Master_Opportunity' AND o.IsWon GROUP BY 1 ORDER BY 1
```
2 rows; first rows: `[{"yr":2025,"won_master":42,"tagged":37,"amt":"19948445.47","tagged_amt":"14381607.02"},{"yr":2026,"won_master":20,"tagged":4,"amt":"15358868","tagged_amt":"4416000"}]`

Snapshot 20260929T163700Z.

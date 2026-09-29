# Reports: Sales and Marketing Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Sales Exec Pipeline [00OKc000001YCspMAG]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2026-04-13
date: Opportunity.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.CreatedDate (Month), Opportunity.Type
aggregates: Sum of Amount, Sum of Closed, Record count

### Opportunities Grouped by Parent [00OKc0000014c1qMAA]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2025-04-01
filters: 1. Opportunity.Parent_Opportunity__c notEqual ""
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Parent_Opportunity__c
aggregates: Sum of Amount, Record count

### Marketing Exec Leads by Source [00OKc000001YCsqMAG]
folder Sales and Marketing Reports · type LeadList · Summary · last run 2023-06-16
date: CREATED_DATE LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
grouped by: Lead.LeadSource, CREATED_MONTH (Day)
aggregates: Record count

### Sales Person Activity [00OKc000001YCsoMAG]
folder Sales and Marketing Reports · type Activity · Summary · last run 2023-03-31
date: Activity.ActivityDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: closed=open, type=te
grouped by: ACCOUNT, Activity.Subject
aggregates: Record count

### Sales Manager Closed Deals [00OKc0000013SqMMAU]
folder Sales and Marketing Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH (Day)
aggregates: Sum of Amount

### Sales Manager Open Pipeline [00OKc000001YCvKMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.CreatedDate (Month), Opportunity.Type
aggregates: Sum of Amount, Sum of Closed, Record count

### Sales Manager Pipeline Next 90 days [00OKc000001YCvLMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CloseDate NEXT_N_DAYS:90 (2026-09-29 to 2026-12-27)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.CreatedDate (Month), Opportunity.StageName
aggregates: Sum of Amount, Sum of Closed, Record count

### Activities by Salesperson [00OKc000001YCuvMAG]
folder Sales and Marketing Reports · type Activity · Matrix · last run 2015-08-07
date: DUE_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
standard: closed=all, type=te
grouped by: Activity.Owner.Name
aggregates: Record count

### Sales Manager Leader Board [00OKc000001YCuyMAG]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name
aggregates: Sum of Amount, Record count

### Sales Manager Top Closed Deals [00OKc000001YCuzMAG]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount, Record count

### Sales Manager Open Opportunities [00OKc000001YCvJMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount, Record count

### Sales Person All Activities [00OKc000001YCvMMAW]
folder Sales and Marketing Reports · type Activity · Matrix · last run 2015-08-04
date: Activity.ActivityDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: closed=all, type=te
grouped by: Activity.ActivityDate (Week), Activity.Status, Activity.ActivityType
aggregates: Record count

### Sales Person Current Month Open Pipeline [00OKc000001YCvBMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-04
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Name
aggregates: Average Probability (%), Sum of Amount, Average Age, Record count

### Sales Person Open Pipeline by stage [00OKc000001YCvOMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-04
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.StageName
aggregates: Sum of Amount, Average Age, Record count

### Sales Person MTD Sales [00OKc000001YCvNMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-04
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount, Record count

### Sales Exec Bookings Trend [00OKc000001YCvDMAW]
folder Sales and Marketing Reports · type Opportunity · Matrix · last run 2015-08-04
date: Opportunity.CloseDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.CloseDate (DayInMonth), CLOSE_MONTH (Day)
aggregates: Sum of Amount, Average Age, Record count

### Marketing Exec Conversion Rate [00OKc000001YCv2MAG]
folder Sales and Marketing Reports · type OpportunityLead · Summary · last run 2015-08-04
date: Lead.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
grouped by: Lead.CreatedDate (Month)
aggregates: Sum of Opportunity Amount, Conversion Rate, Record count
formulas: Conversion Rate: CONVERTED:SUM / RowCount

### Marketing Exec Converted and Won Amount [00OKc000001YCv4MAG]
folder Sales and Marketing Reports · type OpportunityLead · Summary · last run 2015-08-04
filters: 1. CONVERTED equals "True"; 2. STAGE_NAME equals "Closed Won"
date: CONVERTED_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
grouped by: CONVERTED_DATE (Day)
aggregates: Sum of Opportunity Amount, Record count

### Marketing Exec Converted by Month [00OKc000001YCv5MAG]
folder Sales and Marketing Reports · type OpportunityLead · Summary · last run 2015-08-04
filters: 1. CONVERTED equals "True"
date: CONVERTED_DATE LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
grouped by: CONVERTED_DATE (Day)
aggregates: Sum of Opportunity Amount, Record count

### Marketing Exec Lead Trends by Status [00OKc000001YCv6MAG]
folder Sales and Marketing Reports · type LeadList · Matrix · last run 2015-08-04
date: Lead.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
grouped by: Lead.CreatedDate (Month), Lead.Status
aggregates: Record count

### Marketing Exec Leads by Campaigns [00OKc000001YCv8MAG]
folder Sales and Marketing Reports · type CampaignLead · Summary · last run 2015-08-04
grouped by: Campaign.Name, Campaign.CampaignMember.Lead.Owner.Name
aggregates: Record count

### Marketing Exec Leads Converted [00OKc000001YCv7MAG]
folder Sales and Marketing Reports · type LeadList · Matrix · last run 2015-08-04
filters: 1. Lead.IsConverted equals "True"
date: CREATED_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
grouped by: CREATED_MONTH (Day)
aggregates: Sum of Converted, Record count

### Marketing Exec # of Leads [00OKc000001YCv9MAG]
folder Sales and Marketing Reports · type LeadList · Matrix · last run 2015-08-04
date: CREATED_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
grouped by: CREATED_MONTH (Day)
aggregates: Sum of Converted, Record count

### Marketing Exec Campaigns by ROI [00OKc000001YCuxMAG]
folder Sales and Marketing Reports · type CampaignList · Summary · last run 2015-08-04
grouped by: Campaign.Name
aggregates: Sum of ROI, Sum of Value Opportunities in Campaign

### Marketing Exec Campaign ROI by Camp Type [00OKc000001YCuwMAG]
folder Sales and Marketing Reports · type CampaignList · Summary · last run 2015-08-04
grouped by: Campaign.Type
aggregates: Largest ROI, Record count

### Marketing Exec Leads by Industry [00OKc000001YCv0MAG]
folder Sales and Marketing Reports · type LeadList · Summary · last run 2015-08-04
date: CREATED_DATE THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
grouped by: Lead.Industry
aggregates: Record count

### Marketing Exec Converted Amount [00OKc000001YCv3MAG]
folder Sales and Marketing Reports · type OpportunityLead · Summary · last run 2015-08-04
filters: 1. CONVERTED equals "True"
date: CONVERTED_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
grouped by: CONVERTED_DATE (Day)
aggregates: Sum of Opportunity Amount, Record count

### Marketing Exec Amount per Camp [00OKc000001YCv1MAG]
folder Sales and Marketing Reports · type OpportunityCampaign · Summary · last run 2015-08-04
date: CAMPAIGN_STARTDATE LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Campaign.Name, Opportunity.CloseDate (Month), Opportunity.Campaign.Type
aggregates: Sum of Amount, Average Age, Average Amount per Campaign, Record count
formulas: Average Amount per Campaign: AMOUNT:SUM / RowCount

### Sales Exec Opportunity Product Pipeline [00OKc000001YCvAMAW]
folder Sales and Marketing Reports · type OpportunityProduct · Matrix · last run 2015-08-03
date: Opportunity.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.OpportunityLineItem.PricebookEntry.Product2.Name, Opportunity.CreatedDate (Quarter)
aggregates: Sum of Quantity, Sum of Total Price

### Sales Exec Closed Deals by Owner [00OKc000001YCvCMAW]
folder Sales and Marketing Reports · type Opportunity · Matrix · last run 2015-08-03
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name
aggregates: Sum of Amount, Close Rate, Record count
formulas: Close Rate: WON:SUM/RowCount

### Sales Exec Closed Deals QTD [00OKc000001YCvEMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-03
date: CLOSE_DATE THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: CLOSE_MONTH (DayInMonth)
aggregates: Sum of Amount

### Sales Exec Open Pipeline next 90 days [00OKc000001YCvHMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-03
date: Opportunity.CloseDate NEXT_N_DAYS:90 (2026-09-29 to 2026-12-27)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.CreatedDate (Month), Opportunity.StageName
aggregates: Sum of Amount, Sum of Closed, Record count

### Sales Exec Open Deals [00OKc000001YCvGMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-03
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount, Record count

### Sales Exec Lost Deals [00OKc000001YCvFMAW]
folder Sales and Marketing Reports · type Opportunity · Matrix · last run 2015-08-03
filters: 1. Opportunity.StageName equals "Closed Lost"
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Name, Opportunity.Type
aggregates: Sum of Amount

### Sales Exec Top Closed Deals [00OKc000001YCvIMAW]
folder Sales and Marketing Reports · type Opportunity · Summary · last run 2015-08-03
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount, Record count

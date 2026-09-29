# Glossary

Words the business uses, and what they mean in the data.

## Activity / task type
"Activities" in Salesforce reports are Tasks plus Events (type=te). The task type is TaskSubtype (Task, Email, Call, LinkedIn); Task Type and Call fields are never filled. Events have no usable type: Event.Type is never filled and EventSubtype is always Event, so meetings can only be grouped by free-text subject (demo, meeting). "Completed" is Status = Completed (IsClosed = true); Open is the only other status.

Evidence: `q1`, `q30` (see findings/).
  > Reviewer: No cited query reads the Task Type field, the Call fields, or Event.Type, so 'never filled' is unevidenced for all three. Also, going by q1 and q11, the Call subtype appears only in the sample tasks (2 completed Calls). Real data has no Call tasks, which is worth saying so users don't expect a call breakdown.

## Business type (new vs existing), service line, operating entity
Business_Type__c: Exisiting (sic), New, New - RFP (a new client won through a formal RFP), Organic Growth. Service line = Opportunity.Type: Media, Creative, Agency. Operating entity = Operating_Entity__c: which PUSH company owns the work (Push Canada, Push USA, Stratis). It describes PUSH, not the client, and is only reliably filled from FY2026. Client = the Account on the opportunity.

Evidence: `q18`, `q56` (see findings/).
  > Reviewer: "New - RFP (a new client won through a formal RFP)" is wrong in wording. It is the pursuit type: none of the 8 FY2025–26 decided RFP engagements was won, and one sits on an account that had already won. Reword as "a new-business pursuit via a formal RFP".

## Campaign (budget line)
In this org a Campaign is a revenue budget line, not a marketing campaign. There is one tree for 2025: root "2025" -> client node (five named clients plus "New Business") -> service-line leaf ("<client> - Creative / Media / Special Projects"). ExpectedRevenue = budgeted gross revenue, Net_Revenue__c = budgeted net revenue, and engagements (Master Opportunities) are tagged to a leaf through Opportunity.CampaignId. There are no campaign members; lead/contact/response counts are all 0.

Evidence: `q25`, `q42`, `q31` (see findings/).
  > Reviewer: 'There are no campaign members; lead/contact/response counts are all 0' is not shown by the attached queries: q25/q42/q31 do not select NumberOfLeads, NumberOfContacts, NumberOfResponses or CampaignMember. Add evidence or drop that sentence. The tree structure and the leaf tagging via Opportunity.CampaignId are supported.

## Engagement vs project
Engagement = Opportunity with record type Master_Opportunity: the pursuit of a client, and where wins, losses and win rate are counted. Project = record type Sales_Opportunity: a piece of billable work under an engagement (linked through Parent_Opportunity__c), and where revenue is summed. An engagement's Amount is not the sum of its projects, and many won engagements have no project records. The third record type, Stratis, has no records; Stratis work is tagged with Operating_Entity__c = Stratis instead.

Evidence: `q15`, `q22` (see findings/).
  > Reviewer: Two unsupported points. (1) "The third record type, Stratis, has no records" is not backed by any attached query, since none lists record types. (2) Describing a project as "a piece of billable work" is loose: q5 shows 11 Closed Lost and 46 open Sales_Opportunity records, so projects are also pursued and lost. Revenue should be summed only on won projects. Add evidence for the record-type claim and tighten the project definition.

## PUSH Revenue (net revenue)
PUSH's own revenue on a project. For Media it is the media fee (Total_Media_Spend__c × Media_Fee__c); for Creative and Agency it is Amount minus Vendor_Cost__c. It is summed on won Sales Opportunities, in CAD. Gross revenue (Amount) is what the client pays, including pass-through media. See push_revenue and push_revenue_margin.

Evidence: `q8`, `q33` (see findings/).

## Qualified lead = converted lead
Lead Status 'Qualified' is set exactly on converted leads (46 of 46 converted, no unconverted Qualified). 'New Lead' is a separate status used only by the 2026-09-01 list import; 'New' is the status of other open leads. Open statuses: New, New Lead, Working, Nurturing, Internal Debrief.

Evidence: `q2`, `q10` (see findings/).

## Revenue Budget (Sales campaigns)
The yearly revenue budget is kept as Campaigns of Type Sales: a root campaign per year ('2025'), client-level children, and client × service-line leaves (Media, Creative, Special Projects) whose ExpectedRevenue is the budget line. The root equals the sum of the leaves. The middle 'New Business' node repeats its children, so do not sum all children. Only a 2025 budget exists.

Evidence: `q47`, `q54` (see findings/).

## Sales stages and forecast categories
Open stages in use: Discovery (10%, Pipeline), Creds Presentation (25%, Pipeline; added 2026-06-08, a credentials pitch), Proposal (50%, Best Case), Negotiation (75%, Commit; almost never used), Contract (90%, Commit). Closed: Closed Won (100%, Closed) and Closed Lost (0%, Omitted). Kick-off, Project In Progress and Project Completion (plus Financial Setup, never used) are legacy won stages describing delivery status. All four count as IsClosed/IsWon and were deactivated on 2026-06-08. Forecast category always follows the stage on open engagements. Probability is the rep-editable value and can differ from the stage default. 'Commit' is stored as ForecastCategory = 'Forecast' (API value) with ForecastCategoryName = 'Commit'.

Evidence: `q12`, `q64`, `q4` (see findings/).
  > Reviewer: Several parts are not in the evidence. Negotiation's 75%/Commit mapping and 'almost never used' are unsupported: there are no Negotiation rows in q12 or q4, and no history count. So are Financial Setup being 'never used' and counting as IsClosed/IsWon (it has no records, and the stage table's IsWon was not shown), and ForecastCategory='Forecast' as the stored value. 'A credentials pitch' is an interpretation. Mark these as unverified or add the evidence.

## Won, lost, decided
Won = IsWon true, meaning stage Closed Won or any delivery stage (Kick-off, Project In Progress, Project Completion; Financial Setup is defined but unused). Lost = closed and not won (Closed Lost). Decided = IsClosed (won + lost). Open = everything else (Discovery, Creds Presentation, Proposal, Contract).

Evidence: `q5` (see findings/).

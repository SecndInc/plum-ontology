---
name: engagements_created
version: 1
status: accepted
kind: base
owner: revops
description: Engagements (Master Opportunities) created, by created date in the org time zone.
source: {type: manual, ref: ontologies/push-media/salesforce/queries/deal-count.md}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
time_column: CreatedDate
time_semantics: calendar
dimensions:
  - {key: business_type, column: Business_Type__c}
filters:
  - {key: business_type, column: Business_Type__c, type: picklist, allowed_values: [Exisiting, New, New - RFP, Organic Growth]}
topic: bd
format: number
aliases: ["new engagements", "engagements opened", "engagements created"]
---

Most FY2025 engagements were bulk-loaded in May 2025; see [[deal-count]].

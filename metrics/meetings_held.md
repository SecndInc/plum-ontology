---
name: meetings_held
version: 1
status: proposed
kind: base
owner: revops
description: Calendar events (demos, client meetings) logged in Salesforce, by meeting date in the org time zone, excluding sample data and zero-length notes.
source: {type: manual, ref: activity topic investigation q27 q30 q93}
confidence: medium
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["meetings", "events", "demos", "client meetings", "meetings booked"]
grain: event
source_table: Event
measure: {agg: count, column: Id}
base_filters:
  - {field: CreatedById, op: "!=", value: 005Kc0000010gjJIAQ}
  - {field: DurationInMinutes, op: ">", value: 0}
time_column: ActivityDate
time_semantics: fiscal
dimensions:
  - {key: owner_profile, column: Owner.ProfileId, label: Owner profile (role proxy)}
coverage_checks:
  - {name: no_start, sql_predicate: StartDateTime IS NULL, description: Event with no start time; outside any period}
  - {name: no_contact, sql_predicate: WhoId IS NULL, description: Meeting with no contact or lead attached}
  - {name: not_linked, sql_predicate: WhatId IS NULL, description: Meeting not linked to an opportunity or account}
---

Counts Event rows. The Event Type field is never filled and EventSubtype is always "Event", so there is no
type breakdown; the subject is free text (demos, meetings, and 2 events whose subject says an email was sent,
which are emails logged as events).

Dated by ActivityDate, which equals the start date in the org time zone (America/New_York).
2 of the 10 real events start on a different UTC date, so do not date by StartDateTime in UTC.

Excludes the 3 sample events from org setup (created by 005Kc0000010gjJIAQ) and the 2 zero-length
"Audio" notes a System Administrator logged on a non-opportunity record (prefix a09).
Every real event is from 2026, so FY2025 is 0. Held and scheduled are not separated: future-dated events count once their date comes.


## Reviewer note
The name, description and aliases don't match what is counted. (1) It counts the 2 emails logged as events as meetings, which the notes admit. (2) It counts future scheduled events once their date arrives, so it is not 'held'. (3) The alias 'meetings booked' implies dating by when the meeting was booked, but the metric dates by meeting date. Either filter out email-logged events and future dates, or rename it (for example 'events_by_date'), drop the 'meetings booked' alias, and put the email and scheduled-vs-held caveats in the description.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0

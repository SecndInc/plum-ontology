---
name: win_rate
version: 1
status: accepted
kind: derived
owner: revops
description: Share of decided engagements that were won (count-based).
source: {type: manual, ref: ontologies/push-media/salesforce/queries/win-rate.md}
confidence: high
last_verified: 2026-09-29
formula: won_count / closed_count
inputs: [won_count, closed_count]
dimensions:
  - {key: service_line, column: Type}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
topic: bd
format: percent
aliases: ["win rate", "success rate", "win ratio"]
---

Golden G13: FY2025 is 42 won of 52 decided.

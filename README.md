# plum-ontology

Reviewed metric definitions for Plum (Context graph's verified answers over the Salesforce mirror in BigQuery `secnd-ml.stratis_ai`).

Every answer Plum gives cites the commit of this repository it used, so an answer can always be replayed against the exact definition. Nothing becomes trusted without review: changes arrive as pull requests, from people or from Plum's agent, and a person merges them.

## Layout

```
metrics/<name>.md      one metric per file: YAML frontmatter (the definition) + prose (context, caveats, links)
```

Planned, as the sweep and the push-media port land: `objects/`, `reports/`, `paths/`, `glossary.md`, `gotchas.md`.

## A metric file

```yaml
---
name: win_rate                # must equal the file name
version: 1                    # bump on any change to the definition
status: accepted              # proposed | accepted | degraded | deprecated
kind: derived                 # base | derived
owner: revops
description: Share of decided engagements that were won (count-based).
source: {type: manual, ref: ontologies/push-media/salesforce/queries/win-rate.md}
confidence: high
last_verified: 2026-09-29
topic: bd                     # groups suggestions on the Ask screen
format: percent               # number | percent | currency (display only)
aliases: ["win rate", "success rate"]   # words people use; Ask matches them
formula: won_count / closed_count       # derived: metric names, numbers, + - * / and parentheses
inputs: [won_count, closed_count]
dimensions:
  - {key: service_line, column: Type}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
---
```

Base metrics instead declare `grain`, `source_table`, `measure: {agg, column}`, structured `base_filters` (`{field, op, value}`), `time_column`, `time_semantics` (fiscal | calendar), optional `currency: {column, convert}`, `coverage_checks` and `reconcile: {sf_report_id, compare_column, tolerance}`. Columns are Salesforce field paths on the source object: `Field` or `Relationship.Field`. The schema is `PlumMetricSchema` in `shared/src/plum.ts` of context-graph.

## Validate

From a context-graph checkout:

```bash
bun --cwd backend run plum:validate ../plum-ontology
```

CI runs the same check on every push and pull request. It checks out `yuengeoff/context-graph`, which is private, so the repository needs an Actions secret `CONTEXT_GRAPH_READ_TOKEN`: a fine-grained token with read access to that repository's contents.

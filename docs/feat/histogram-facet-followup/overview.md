# Histogram Facet Followup Overview

## Problem Statement

This plan tracks the local follow-up work that remains after retargeting
`feat/histogram-facet-followup` to `upstream/dev`. Earlier histogram facet
development through Task CR.10 has been merged and moved to
`docs/feat/histogram-facet/`.

## Project Context

- Environment: `conda activate spac`
- Feature branch: `feat/histogram-facet-followup`
- Target branch: `upstream/dev`
- Current local code delta from `upstream/dev`: `6993169` and `af99c25`
- Scope: histogram excessive-group filtering/warnings and histogram title
  ownership consistency
- Primary files in the local delta:
  - `src/spac/visualization.py`
  - `src/spac/templates/histogram_template.py`
  - `tests/test_visualization/test_histogram.py`
  - `tests/templates/test_histogram_template.py`
- Detailed records:
  - [Task Details](./development-details/task-details.md)
  - [Decisions](./development-details/decisions.md)
  - [Implementation Log](./development-details/implementation-log.md)
  - [Implementation Notes](./development-details/implementation-notes.md)
  - [Future Work](./future-work.md)

---

## Immediate Next Step

Review the cleaned follow-up documentation and then prepare the CR.11/CR.12
changes for commit and PR review.

## Progress

### Ongoing Tasks
None currently.

### Remaining Tasks
None currently.

### Postponed Tasks
None currently.

### Dropped Tasks
None currently in the local-only follow-up scope.

### Addressed Tasks
CR.12. Histogram Title Ownership and Facet Title Consistency.
CR.11. Excessive Group Filtering With User Warning.

### Merged Historical Tasks
Tasks CR.1-CR.10 and numbered Tasks 1-22 are already part of the merged
histogram facet history and are preserved under `docs/feat/histogram-facet/`.

### Issues (Open)
None currently.

---

## Analysis Summary

### Current Local Code Delta
1. Histogram core and template warning behavior:
   - Grouped histograms that exceed `max_groups` now render the most frequent
     groups instead of failing fast.
   - Omitted groups are filtered from plotting data so they do not affect
     shared numeric bins or categorical slots.
   - Core `histogram()` emits a `UserWarning`; the histogram template captures
     and logs that warning for template users.
2. Histogram title ownership and wording:
   - Core owns per-axis titles for direct-call, grouped, and facet paths.
   - Template owns figure-level titles, with a single-axis template exception
     for better UX.
   - Template multi-axis paths no longer recompute raw groups to overwrite
     core panel titles, preserving consistency after `max_groups` filtering.
   - Title wording is compact and consistently uses "Histogram", with table or
     layer context only where it clarifies feature plots.
3. Focused test state from the latest log:
   - `tests/test_visualization/test_histogram.py` and
     `tests/templates/test_histogram_template.py` passed together
     (`46 passed, 2 warnings`) for the CR.12 snapshot.

### Codebase Pattern Findings (Concise)
1. Template layer owns user-facing parameter normalization and UX logging.
2. Core plotting functions should expose direct Python/API warnings for
   behavior that changes plotted data.
3. Template-level titles should not overwrite core-rendered panel titles when
   the core can filter or transform the plotted groups.

---

## Development Details
See [task-details.md](./development-details/task-details.md) for the local-only
task record.

## Decision Log
See [decisions.md](./development-details/decisions.md) for the local-only
decision history and rationale record.

## Execution Log
See [implementation-log.md](./development-details/implementation-log.md) for
the local-only dated implementation and verification history.

---

## Future Work
See [future-work.md](./future-work.md) for deferred follow-up ideas and
out-of-scope notes.

---

## Implementation Notes
See [implementation-notes.md](./development-details/implementation-notes.md)
for follow-up-specific implementation notes. Follow `CONTRIBUTING.md` for
repo-wide requirements and `spac-dev-guide` for reusable SPAC development
heuristics.

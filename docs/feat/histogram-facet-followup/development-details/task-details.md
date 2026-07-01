# Task Details

## Code Review

### Task CR.12. Histogram Title Ownership and Facet Title Consistency
Location: src/spac/visualization.py, src/spac/templates/histogram_template.py, tests
Date: 2026-06-09
Last updated: 2026-06-30

Status: Done

Implementation remarks:
- Convert the former open facet-title inconsistency issue into active review
  follow-up work.
- Keep user-facing wording concise: use "Histogram" everywhere, include table
  context only for feature plots, and avoid redundant "Layer", "Group", or
  "Count plot" wording in final titles.
- Core owns per-axis titles. The template owns figure-level titles, with a
  single-axis exception where the template may set the per-axis title for
  better UX.
- Multi-axis template paths must not recompute groups from raw `adata.obs` to
  overwrite core panel titles, because core may filter groups before plotting.
- Final implementation keeps template title construction next to title
  assignment so the figure-level title behavior is easy to read and revise.
- Latest wording refinement keeps core and template titles compact: feature
  plots add table context in parentheses, grouped overlays say "grouped by",
  and facet figures say "faceted by" while leaving panel titles core-owned.
- The added template title smoke coverage is sufficient for the current
  follow-up; no additional template-only tests are needed for this PR.

Action items:
- [x] Define simplified histogram title wording for feature and annotation
  plots across core and template paths.
- [x] Update core direct-call per-axis titles to use concise histogram wording.
- [x] Update template title handling so figure-level titles carry template
  context and multi-axis panel titles remain core-owned.
- [x] Remove template-side raw-group title reassignment from facet/grouped
  separate paths.
- [x] Add a small template test that verifies a figure title exists without
  constraining the title content.
- [x] Run focused histogram and histogram-template tests.

### Task CR.11. Excessive Group Filtering With User Warning
Location: src/spac/visualization.py, tests/test_visualization/test_histogram.py
Date: 2026-06-09

Status: Done

Implementation remarks:
- Convert the former open Issue 3 into active review follow-up work.
- Desired user behavior: when grouped plots exceed `max_groups`, continue
  plotting by selecting the most frequent `max_groups` groups and warn users
  clearly that groups were omitted.
- UX is the primary concern because silently changing plotted groups would be
  misleading; implementation readability is second and should be kept minimal
  without weakening the warning behavior.
- Keep this scoped to grouped histogram behavior and focused tests. Do not use
  this task for formatting cleanup, line-ending normalization, or unrelated
  plotting refactors.
- Final implementation keeps core behavior minimal and user-facing:
  `histogram()` emits a `UserWarning`, while the histogram template captures
  that warning and logs it for template users.

Action items:
- [x] Replace the excessive-group rejection path with top-frequency group
  selection for grouped histogram plotting.
- [x] Filter plotting data to selected groups so omitted groups do not affect
  shared numeric bins or categorical slots.
- [x] Emit a user-visible warning when groups are omitted.
- [x] Add focused tests with uneven group frequencies to verify top-group
  selection and warning behavior.
- [x] Verify the focused histogram/facet/template test set after the initial
  implementation slice.
- [x] Refine the implementation for minimal diff/readability while preserving
  the user-facing behavior.
- [x] Decide the final warning channel/message policy for this behavior and
  update the code/tests if needed.

## Development

No local-only numbered development tasks remain after retargeting this
follow-up branch to `upstream/dev`. Numbered Tasks 1-22 and review Tasks CR.1
through CR.10 are treated as merged history and are preserved under
`docs/feat/histogram-facet/`.

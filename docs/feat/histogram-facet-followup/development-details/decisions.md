# Decisions

### D55. Split Implementation Notes by Ownership
Date: 2026-06-30
Decision:
Split the old overview implementation notes by their proper ownership layer.

Details:
- Keep repo-wide SPAC requirements in `CONTRIBUTING.md` and reference them
  instead of duplicating them in this follow-up overview.
- Move reusable SPAC development heuristics into the new `spac-dev-guide`
  skill so they can apply beyond this feature branch.
- Keep only histogram-facet/follow-up-specific notes in
  `development-details/implementation-notes.md`.
- Keep `overview.md` as an index/summary with pointers to companion records.

Rationale:
The previous overview notes mixed repo-wide policy, reusable development
heuristics, and feature-specific guidance. Splitting them keeps the follow-up
plan lighter while preserving the guidance at the layer where it is reusable.

### D54. Do Not Track Whitespace-Only Cleanup for Follow-Up PR
Date: 2026-06-30
Decision:
Do not treat whitespace-only cleanup as part of the current histogram facet
follow-up PR scope.

Details:
- Do not add a task for clearing historical whitespace reports.
- Do not use whitespace-only edits to force a clean local `git diff --check`
  when those edits are not part of the reviewer-facing PR diff.
- Keep the follow-up documentation focused on CR.11 excessive-group filtering
  and CR.12 title ownership.

Rationale:
Whitespace cleanup is not meaningful for the current PR review and will not
appear in the git PR diff.

### D53. Close Remaining Histogram Follow-Up Questions
Date: 2026-06-30
Decision:
Close the remaining open histogram-facet review questions without adding new
implementation scope.

Details:
- George's question about whether `shrink`, `bins`, `alpha`, and `stat` were
  removed from the histogram template contract is resolved by clarification:
  those parameters were not removed.
- The template test scope question is resolved by the added template title
  smoke coverage. No additional template-only tests are needed for the current
  follow-up PR.
- Keep broader template-test expansion out of scope unless a future bug or
  review request identifies a specific template-owned behavior gap.

Rationale:
The current focused tests cover the remaining title-ownership follow-up, and
the resolved parameter-contract question does not require code or test changes.

### D52. Unify Histogram Title Ownership and Wording
Date: 2026-06-09
Decision:
Adopt simplified histogram title wording and split title ownership between
core and template layers.

Details:
- Use "Histogram" for histogram outputs; do not introduce "Count plot" titles.
- Use `layer` wording for direct core calls and `table` wording for
  template-facing titles.
- Include table/layer context for feature plots, but omit table/layer context
  for annotation plots.
- Core owns per-axis titles, including facet and grouped-panel titles.
- Template owns figure-level titles. For single-axis template plots, the
  template may also set the per-axis title for better user experience.
- Template multi-axis paths should not recompute groups from raw `adata.obs`
  to overwrite core panel titles, because core may filter groups before
  plotting.
- Add only a small template title-existence test, without constraining exact
  figure-title content.

Rationale:
This keeps final titles user-friendly while avoiding the Y.11-style facet
title mismatch where template-level raw groups disagree with core-rendered
groups after `max_groups` filtering.

### D51. Split Excessive Group Warnings by Layer
Date: 2026-06-09
Decision:
For excessive grouped histogram filtering, keep `histogram()` responsible for
emitting a Python `UserWarning`, and keep the histogram template responsible
for logging captured core warnings for template users.

Details:
- Core `histogram()` should not call `logging.warning(...)` for this behavior.
- Direct Python/API users should see a normal `UserWarning`.
- Template users should see the same behavior surfaced through the template
  logger, because Python warnings may not be visible in template/JSON/Shiny
  workflows.
- The warning is part of the user-facing plotting contract because filtering
  omitted groups materially changes plot interpretation.

Rationale:
This matches the codebase's layer boundary: core/library code uses Python
warnings for API behavior, while templates use logging for template-facing
runtime messages.

### D50. Convert Excessive Group Handling Issue Into Task CR.11
Date: 2026-06-09
Decision:
Convert the open excessive-group future-work issue into `Task CR.11`, scoped
as grouped histogram top-frequency filtering with a user-visible warning.

Details:
- Replace the previous reject-only behavior when grouped plots exceed
  `max_groups` with plotting the most frequent `max_groups` groups.
- Keep the behavior user-friendly: the plot should still render, but users
  must be clearly warned because omitted groups materially change the plotted
  result.
- Keep implementation scope narrow: grouped histogram behavior, focused
  tests, and wording/docstring alignment only.
- Preserve review cleanliness: do not use this task for formatting cleanup,
  line-ending normalization, or unrelated refactors.
- Leave the final minimal-code structure and warning-channel policy open until
  the intermediate implementation is reviewed.

Rationale:
This follows George's preference from CR.10 to avoid an `"unlimited"` escape
hatch and instead provide a safer top-N grouped plotting behavior. The warning
is part of the UX contract because filtering changes plot interpretation.

## Merged History

Decisions D1-D49 are treated as merged history after retargeting this
follow-up branch to `upstream/dev`. They remain preserved under
`docs/feat/histogram-facet/`.

# Implementation Notes

These notes are specific to the current histogram facet follow-up. Repo-wide
SPAC requirements remain governed by `CONTRIBUTING.md`; reusable SPAC
development heuristics live in the `spac-dev-guide` skill.

## Current Scope

- Keep this PR focused on CR.11 excessive-group filtering and CR.12 title
  ownership.
- Do not use this follow-up for whitespace-only cleanup or broad formatting
  churn.

## Histogram Facet Notes

- Allow cross-mode consistency tests when they protect shared behavior
  introduced by histogram facet changes.
- Keep facet test ordering readable: smoke/core behavior first, layout-hint
  contracts next, deeper consistency/regression checks last.
- Preserve the CR.12 title boundary: core owns per-axis/panel titles; template
  owns figure-level titles and should not recompute raw groups to overwrite
  core-rendered panels.

## Verification

- Run focused histogram/template tests after code changes:
  `python -m pytest tests/test_visualization/test_histogram.py tests/templates/test_histogram_template.py`

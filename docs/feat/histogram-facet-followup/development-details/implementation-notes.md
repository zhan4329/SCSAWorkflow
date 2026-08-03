# Implementation Notes

These notes are specific to the current histogram facet follow-up. Repo-wide
SPAC requirements remain governed by `CONTRIBUTING.md`; reusable SPAC
development heuristics live in the `spac-dev-guide` skill.

## Current Scope

- This follow-up records CR.11-CR.14 histogram filtering and title behavior.
- The latest completed slice covers CR.13 title examples and CR.14 filtered
  top-N title suffixes.
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

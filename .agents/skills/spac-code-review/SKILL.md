---
name: spac-code-review
description: "Use when reviewing SPAC code changes, pull requests, or diffs. Applies CONTRIBUTING.md requirements for SPAC terminology, AnnData semantics, tests, error handling, figures, docs, and PR readiness. Triggers: code review, PR review, reviewer comments, review this diff, review this change."
author: Boqian Zhang
version: 2026.4.21
---

# SPAC Code Review

Use this skill when reviewing SPAC code changes, pull requests, or diffs.

When wording below comes from `CONTRIBUTING.md`, keep it exact.

## Review Output

- Default to a code-review mindset: prioritize bugs, behavioral regressions, missing tests, and missing docs.
- Present findings first, ordered by severity, with file and line references when available.
- Keep summaries brief and secondary to findings.
- If no findings are discovered, say so explicitly and note any residual testing or validation gaps.

## Review Against CONTRIBUTING.md

### Pull Request Guidelines

- When you're done making changes, check that your changes conform to any code formatting requirements and pass any tests.
- The pull request should include additional tests if appropriate.
- If the pull request adds functionality, the docs should be updated.
- The pull request should work for all currently supported operating systems and versions of Python.

### SPAC Terminology

- **Cells:** Rows in the `X` matrix of AnnData.
- **Features:** Columns in the `X` matrix of AnnData, representing gene expression or antibody intensity.
- **Tables:** Originally called **layers** in AnnData, these represent transformed features.
- **Associated Tables:** Corresponds to `.obsm` in AnnData and can store spatial coordinates, UMAP embeddings, etc.
- **Annotation:** Corresponds to `.obs` in AnnData and can store cell phenotypes, experiment names, slide IDs, etc.

### See CONTRIBUTING.md for more guidelines on tests, error handling, figures, and documentation.

## Code Quality Checklist from CONTRIBUTING.md

- [ ] Code organization and modularity:
  - Code is modular and functions do one thing.
  - Core functionalities that work with numpy/dataframes are isolated from high-level functions that deal with AnnData.
  - Functions that change AnnData or dataframes in place do not return that object.
  - Reusable utility functions are placed in `utils/` when generic enough across multiple modules.
- [ ] Code follows the PEP 8 style guide, including:
  - Use 4 spaces for indentation.
  - Use blank lines to separate functions and classes.
  - Limit lines to 79 characters.
  - Organize imports: standard library -> third-party -> local application imports, with a blank line between each group.
- [ ] Documentation:
  - All functions have docstrings following the numpy style guide, including clear parameter descriptions, return values, and examples when appropriate.
  - Docstring lines are limited to 72 characters.
  - Variable names and function names are descriptive.
- [ ] All figures include axis names and titles, with programmatic labeling that reflects the data labels dynamically.
- [ ] All contributed code has unittests in the appropriate `tests/` directory.
  - There should be a test for each file and function, covering simple scenarios, corner cases, handled exceptions, and comprehensive code paths.
  - Ground truth is hard coded with comments explaining the rationale.
  - Test names are descriptive and setups are concise, prioritizing quick comprehension.
- [ ] Error handling is implemented:
  - Utility functions for exception handling from `src/utils.py` are reused when applicable.
  - Error messages include enough context on what is expected and what has been entered, with user-entered values surrounded by double quotes.
  - Warning and error messages follow the specified format.
- [ ] Code is readable by data scientists.

## Review Workflow

### A) Reviewing a Diff or PR

1. Inspect the changed files and infer the affected user-facing behavior. If not specified, check git diff against `upstream/dev` branch (if not available, `main` branch).
2. Open surrounding implementation for local context.
3. Open matching tests and any touched docs.
4. Check the change against every relevant requirement above.
5. Report actionable findings only.
6. Call out verification gaps when tests or docs are missing.

### B) Reviewing a Single File or Function

1. Read the implementation and nearby helpers or callers.
2. Locate corresponding tests.
3. Check for violations of the `CONTRIBUTING.md` requirements above.
4. Report findings with concrete impact.

## Severity Guide

- High: incorrect results, broken API behavior, silent data corruption, missing required validation, or misleading visualization output
- Medium: regression risk, missing required tests/docs, inconsistent inplace behavior, or violating documented SPAC conventions
- Low: maintainability issues likely to cause future bugs or reviewer confusion

## Output Template

Findings:
1. `[high]` `path:line` - issue and why it matters
2. `[medium]` `path:line` - issue and why it matters

Open questions or assumptions:
- ...

If no findings:
- `No blocking findings.`
- `Residual risk:` ...

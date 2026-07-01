# Future Work

This file owns deferred follow-up ideas and out-of-scope notes for the
histogram facet follow-up PR. The overview links here instead of duplicating
the list.

### Immediate Next Steps

- Follow-up for the naming inconsistency between template and tests (email George)
- Remove the deprecated plotting mode for together=False, facet=False
- Possible improvement on `derive_facet_geometry` helper
- Do not reject `ax` directly. Provide it in core function (for facet we can just provide our plotting)

### More Ideas

- Allow abbreviation of labels, label-level fontsize setting (current examples are in Shiny side, `feat_vs_anno` tab (hierachical heatmap)) for long-label issues
- More plot-related data in output dataframe, e.g. frequency/proportion if specified in `stat`
- `kwargs` expansion:
  - Allow more seaborn `kwargs`;
  - Allow more values for existing `kwargs`;
  - A special case is `KDE`: this requires raw data plotting rather than pre-computed hist data by `calculate_histogram` function.
- Possible simplification/reloation for helper functions (need evaluation)
- Possible simplification for facet geometry/layout derivation (need evaluation). Current way is driven by AI

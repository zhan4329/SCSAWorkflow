# Comparisons for Wrapping in PR #434

These examples show the title layout before and after the wrapping change in [SCSAWorkflow PR #434](https://github.com/FNLCR-DMAP/SCSAWorkflow/pull/434). The figures on the left use the previous title layout; the figures on the right use the new line break. All examples plot the `CD25` Feature.

The figures were generated from the Histogram test notebook using the same dataset and settings: [before](https://github.com/zhan4329/SCSAWorkflow/blob/fc0885535ea6bb00f8579257b164529bc2d0784b/notebooks/histogram/test_histogram-text-clipping-spac.ipynb) and [after](https://github.com/zhan4329/SCSAWorkflow/blob/ad608cbedb172782862828de2cd020a8e17f0300/notebooks/histogram/test_histogram-text-clipping-spac.ipynb).

Custom title examples are not included in this file. You may refer to the [latest notebook](https://github.com/zhan4329/SCSAWorkflow/blob/d912a455e70fd838084b351e0695470154ebc8db/notebooks/histogram/test_histogram-text-clipping-spac.ipynb) for how the [cited custom-title image](./histogram_after-custom.png) in the PR summary is generated.

## Original Table

### Grouped

The grouping details are separated from the Feature name.

![Grouped Histogram with the Original Table, before and after](./comparison_grouped.png)

### Grouped with filtering

The grouping and filtering details are separated together from the Feature name. This example displays the 20 most frequent groups out of 731.

![Filtered grouped Histogram with the Original Table, before and after](./comparison_grouped-filtered.png)

## Named Table

The following examples use the `arcsinh_percentile` Table. Its name remains with the Feature name in the title.

### Grouped

![Grouped Histogram with a named Table, before and after](./comparison_table-grouped.png)

### Grouped with filtering

This example displays the 20 most frequent groups out of 731.

![Filtered grouped Histogram with a named Table, before and after](./comparison_table-grouped-filtered.png)

Full-resolution images: [before](./histogram_before.png) and [after](./histogram_after-wrap.png).

## Named Table faceted with filtering

The faceting and filtering details are separated from the Feature and Table names. This example displays the 6 most frequent facets out of 731.

![Filtered faceted Histogram with a named Table, before and after](./comparison_table-faceted-filtered.png)

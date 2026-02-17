# Summary

## Core schema (shared across all modalities)

**AnnData.h5ad**
* [`AnnData.raw.X`](#x-matrix-layers) [`scipy.sparse.csr_matrix`] - Main dataset. Raw counts (not normalized). Fix the dimension for all other metadata. Contains all genes and filtered cells.
* [`AnnData.X`](#x-matrix-layers) - Main dataset. Normalized counts. Should be the same dimension than `AnnData.raw.X`. **Exception** (not recommended):  if `AnnData.raw.X` is NOT provided, it can be the raw count matrix.
* [`AnnData.obs`](#obs-cell-metadata) - Cell metadata. Describe each cell in the dataset.
  * [`index`](#index-of-pandasdataframe) [`str`] - The index of the pandas.DataFrame MUST contain unique identifiers for observations.
  * [`array_col`](#array_col) - 
* [`obsm` (Embeddings)](#obsm-embeddings), which describe each embedding in the dataset
* [`obsp`](#obsp), which describe pairwise annotation of observations
* [`var` and `raw.var` (Gene metadata)](#var-and-rawvar-gene-metadata), which describe each gene in the dataset
* [`varm`](#varm), which describe multi-dimensional annotation of variables/features
* [`varp`](#varp), which describe pairwise annotation of variables/features
* [`uns` (Dataset metadata)](#uns-dataset-metadata), which describe the dataset as a whole

## Spatial data (Visium)

If no description -> same as core

* [`AnnData.raw.X`](#x-matrix-layers)
* [`AnnData.X`](#x-matrix-layers)
* [`AnnData.obs`](#obs-cell-metadata)
  * [`index`](#index-of-pandasdataframe)
  * **[`array_col`](#array_col)** [`int`] - Value of the column coordinate for the corresponding spot from the `array_col` field in `tissue_positions_list.csv` or `tissue_positions.csv`.
  * **[`array_row`](#array_row)** [`int`] - Value of the row coordinate for the corresponding spot from the `array_row` field in in `tissue_positions_list.csv` or `tissue_positions.csv`.

# Forked from

- [schema.md](https://github.com/chanzuckerberg/single-cell-curation/blob/main/schema/7.1.0/schema.md)
- Last updated on Jan, 14 2026
- [Latest commit](https://github.com/chanzuckerberg/single-cell-curation/commit/65b419f55c403ab6809874a56e48fc1406c14148)

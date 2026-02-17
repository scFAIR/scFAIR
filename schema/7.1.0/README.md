# Forked from

- [schema.md](https://github.com/chanzuckerberg/single-cell-curation/blob/main/schema/7.1.0/schema.md)
- Last updated on Jan, 14 2026
- [Latest commit](https://github.com/chanzuckerberg/single-cell-curation/commit/65b419f55c403ab6809874a56e48fc1406c14148)

# Summary

## Core schema (shared across all modalities)

**AnnData.h5ad**
* [`AnnData.raw.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers) [`scipy.sparse.csr_matrix`] - Main dataset. Raw counts (not normalized). Fix the dimension for all other metadata. Contains all genes and filtered cells.
* [`AnnData.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers) - Main dataset. Normalized counts. Should be the same dimension than `AnnData.raw.X`. **Exception** (not recommended):  if `AnnData.raw.X` is NOT provided, it can be the raw count matrix.
* [`AnnData.obs`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obs-cell-metadata) - Cell metadata. Describe each cell in the dataset.
  * [`index`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#index-of-pandasdataframe) [`str`] - The index of the pandas.DataFrame MUST contain unique identifiers for observations.
  * [`assay_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#assay_ontology_term_id) [`str`] - EFO term describing the assay. e.g. `"EFO:0022605"` for *10x 5' v3*.
  * [`cell_type_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#cell_type_ontology_term_id) [`str`] - CL term (or `"unknown"`) describing the curated cell-type. e.g. `"CL:0000115"` for *endothelial cell*. Only present if `uns['is_pre_analysis'] = False`. Can be a UBERON cross-referenced species-specific ontology term such as `"FBbt:00046052"` for *fat cell* in flies.
  * [`development_stage_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#development_stage_ontology_term_id) [`str`] - UBERON term (or `"unknown"`, or `"na"` if `tissue_type` is `"cell line"`) describing the curated developmental stage. e.g. `"UBERON:0000068"` for *embryo stage*. Can be a UBERON cross-referenced species-specific ontology term such as `"FBdv:00007077"` for *day 2 of adulthood* in flies.
* [`obsm` (Embeddings)](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obsm-embeddings), which describe each embedding in the dataset
* [`obsp`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obsp), which describe pairwise annotation of observations
* [`var` and `raw.var` (Gene metadata)](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#var-and-rawvar-gene-metadata), which describe each gene in the dataset
* [`varm`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#varm), which describe multi-dimensional annotation of variables/features
* [`varp`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#varp), which describe pairwise annotation of variables/features
* [`uns` (Dataset metadata)](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#uns-dataset-metadata), which describe the dataset as a whole

## Spatial data (Visium)

If no description -> same as core

* [`AnnData.raw.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers)
* [`AnnData.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers)
* [`AnnData.obs`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obs-cell-metadata)
  * [`index`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#index-of-pandasdataframe) [`str`]
  * **[`array_col`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#array_col)** [`int`] - Value of the column coordinate for the corresponding spot from the `array_col` field in `tissue_positions_list.csv` or `tissue_positions.csv`.
  * **[`array_row`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#array_row)** [`int`] - Value of the row coordinate for the corresponding spot from the `array_row` field in in `tissue_positions_list.csv` or `tissue_positions.csv`.
  * [`assay_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#assay_ontology_term_id) [`str`]
  * [`cell_type_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#cell_type_ontology_term_id) [`str`]
  * [`development_stage_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#development_stage_ontology_term_id) [`str`]
  * 


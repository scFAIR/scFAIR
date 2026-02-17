# Forked from

- [schema.md](https://github.com/chanzuckerberg/single-cell-curation/blob/main/schema/7.1.0/schema.md)
- Last updated on Jan, 14 2026
- [Latest commit](https://github.com/chanzuckerberg/single-cell-curation/commit/65b419f55c403ab6809874a56e48fc1406c14148)

# Summary

## Core schema (shared across all modalities)

**Note:** Terms in italic are auto-filled by the CZI CELLxGENE submission pipeline. scFAIR schema still consider them as required. They should match their ontology id paired field.

**AnnData.h5ad**
* [`AnnData.raw.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers) [`scipy.sparse.csr_matrix`] - Main dataset. Raw counts (not normalized). Fix the dimension for all other metadata. Contains all genes and filtered cells.
* [`AnnData.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers) - Main dataset. Normalized counts. Should be the same dimension than `AnnData.raw.X`. **Exception** (not recommended):  if `AnnData.raw.X` is NOT provided, it can be the raw count matrix.
* [`AnnData.obs`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obs-cell-metadata) - Cell metadata. Describe each cell in the dataset.
  * [`index`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#index-of-pandasdataframe) [`str`] - The index of the pandas.DataFrame MUST contain unique identifiers for observations.
  * [`assay_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#assay_ontology_term_id) [`str`] - EFO term describing the assay. e.g. `"EFO:0022605"` for *10x 5' v3*.
  * *[`assay`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#assay)* [`str`] (Paired with `assay_ontology_term_id`) - Human-readable name assigned to the value of `assay_ontology_term_id`.
  * [`cell_type_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#cell_type_ontology_term_id) [`str`] - CL term (or `"unknown"`) describing the curated cell-type. e.g. `"CL:0000115"` for *endothelial cell*. Only present if `uns['is_pre_analysis'] = False`. Can be a cross-referenced species-specific ontology term such as `"FBbt:00046052"` for *fat cell* in flies.
  * [`development_stage_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#development_stage_ontology_term_id) [`str`] - UBERON term (or `"unknown"`, or `"na"` if `tissue_type` is `"cell line"`) describing the curated developmental stage. e.g. `"UBERON:0000068"` for *embryo stage*. Can be a UBERON cross-referenced species-specific ontology term such as `"FBdv:00007077"` for *day 2 of adulthood* in flies.
  * [`disease_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#disease_ontology_term_id) [`str`] - `"PATO:0000461"` for *normal* or *healthy*, or MONDO term. Can be multiple terms in ascending lexical order separated by the delimiter `" || "` with no duplication of identifiers e.g. `"MONDO:0004604 || MONDO:0043004"`.
  * [`donor_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#donor_id) [`str`] - Identifies unique individuals (or `"pooled"`, or `"unknown"`, "or `"na"` if `tissue_type` is `"cell line"`)
  * [`experimental_condition_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#experimental_condition_ontology_term_id) [`str`] - Terms(s) from CHEBI, EFO, uniprot, or anti-uniprot (or `"na"`) to describe experimental conditions. Can be multiple terms in ascending lexical order separated by the delimiter `" || "` with no duplication of identifiers.
  * [`is_primary_data`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#is_primary_data) [`bool`] - True or False depending on origin. For meta-analyses or integration study it should be False.
  * [`self_reported_ethnicity_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#self_reported_ethnicity_ontology_term_id) [`str`] - HANCESTRO term (or "unknown") only if organism is human ("na" for other organisms or if `tissue_type` is `"cell line"`).
  * [`sex_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#sex_ontology_term_id) [`str`] - One of `"PATO:0000383"` for female, `"PATO:0000384"` for male, or `"PATO:0001340"` for hermaphrodite (or "unknown", or "na" if `tissue_type` is `"cell line"`.
  * [`suspension_type`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#suspension_type) [`str`] - One of `"cell"`, `"nucleus"`, or `"na"`. Should match with selected `assay`.
  * [`tissue_type`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#tissue_type) [`str`] - One of `"tissue"`, `"organoid"`, `"cell line"`, or `"primary cell culture"`.
  * [`tissue_ontology_term_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#tissue_ontology_term_id) [`str`] - UBERON term if `tissue_type` is `"tissue"` or `"organoid"`. Cellosaurus term if `tissue_type` is `"cell line"`, or CL term if `tissue_type` is `"primary cell culture"`.

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
  * *<Same as core>*
  * **[`array_col`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#array_col)** [`int`] - Value of the column coordinate for the corresponding spot from the `array_col` field in `tissue_positions_list.csv` or `tissue_positions.csv`.
  * **[`array_row`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#array_row)** [`int`] - Value of the row coordinate for the corresponding spot from the `array_row` field in in `tissue_positions_list.csv` or `tissue_positions.csv`.
  * **[`in_tissue`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#in_tissue)** [`int`] - Value for the corresponding spot from the in_tissue field in `tissue_positions_list.csv` or `tissue_positions.csv` which is either 0 if the spot falls outside tissue or 1 if the spot falls inside tissue.

## Perturbation study

If no description -> same as core

* [`AnnData.raw.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers)
* [`AnnData.X`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#x-matrix-layers)
* [`AnnData.obs`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#obs-cell-metadata)
  * *<Same as core>*
  * **[`genetic_perturbation_id`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#genetic_perturbation_id)** [`str`] - `"na"` or one or more genetic perturbation identifiers in ascending lexical order separated by the delimiter `" || "` with no duplication of identifiers.
  * **[`genetic_perturbation_strategy`](https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md#genetic_perturbation_strategy)** [`str`] - One of `"control"`, `"CRISPR activation screen"`, `"CRISPR interference screen"`, `"CRISPR knockout mutant"`, or `"CRISPR knockout screen"` (or `"no perturbations"` if `genetic_perturbation_id` is `"na"`).


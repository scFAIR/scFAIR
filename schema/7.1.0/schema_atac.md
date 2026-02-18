# Schema

Contact: vincent.gardeux@epfl.ch

Document Status: _Drafting_

Version: 7.1.0_scfair

Current schema: **atac**

## Schema split

The scFAIR schema is split into multiple part, to differentiate the metadata specific to certain modalities:
- The **core** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md]('schema.md') is the main schema for all types of single-cell data (scRNA-seq, scATAC-seq, perturbation, spatial, ...). It describes the core metadata between all modalities.
- The **spatial** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_spatial.md]('schema_spatial.md') describes the additional metadata that are specific to spatial datasets (Visium)
- The **perturb** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_perturb.md]('schema_perturb.md') describes the additional metadata that are specific to perturbation datasets (CRISPR screens, perturb-seq, ...)
- This **atac** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_atac.md]('schema_atac.md') describes the additional metadata that are specific to scATAC datasets (scATAC-seq, multiomics)

## `X` (Matrix Layers)

<b>paired assay</b>. `assay_ontology_term_id` is a descendant of both <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0010891"><code>"EFO:0010891"</code></a> for <i>scATAC-seq</i> and <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0008913"><code>"EFO:0008913"</code></a> for <i>single-cell RNA sequencing</i>. A gene expression matrix (RNA data) is required.

<b>unpaired assay</b>. `assay_ontology_term_id` is <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0010891"><code>"EFO:0010891"</code></a> for <i>scATAC-seq</i> or a descendant and is not a descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0008913"><code>"EFO:0008913"</code></a> for <i>single-cell RNA sequencing</i>. A gene activity matrix and not a peak matrix is required.

Also see the requirements for [scATAC-seq assets](#scatac-seq-assets).<br><br>

The following table describes the matrix data and layers requirements that are **assay-specific**. If an entry in the table is empty, the schema does not have any other requirements on data in those layers beyond the ones listed above.

| Assay | "raw" required? | "raw" location | "normalized" required? | "normalized" location |
|-|-|-|-|-|
| paired scRNA-seq (e.g. 10x multiome) | REQUIRED. Values MUST be de-duplicated molecule counts. Each cell MUST contain at least one non-zero value. All non-zero values MUST be positive integers stored as `numpy.float32`. Any two cells MUST NOT contain identical values for all their features. | `AnnData.raw.X` unless no "normalized" is provided, then `AnnData.X` | STRONGLY RECOMMENDED | `AnnData.X` |
| unpaired Accessibility (e.g. ATAC-seq, mCT-seq) | NOT REQUIRED | | REQUIRED | `AnnData.X` | STRONGLY RECOMMENDED |


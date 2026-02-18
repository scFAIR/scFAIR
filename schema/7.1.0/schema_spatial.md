# Schema

Contact: vincent.gardeux@epfl.ch

Document Status: _Drafting_

Version: 7.1.0_scfair

Current schema: **spatial**

## Schema split

The scFAIR schema is split into multiple part, to differentiate the metadata specific to certain modalities:
- The **core** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md]('schema.md') is the main schema for all types of single-cell data (scRNA-seq, scATAC-seq, perturbation, spatial, ...). It describes the core metadata between all modalities.
- This **spatial** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_spatial.md]('schema_spatial.md') describes the additional metadata that are specific to spatial datasets (Visium)
- The **perturb** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_perturb.md]('schema_perturb.md') describes the additional metadata that are specific to perturbation datasets (CRISPR screens, perturb-seq, ...)

## `obs` (Cell Metadata)

`obs` is a [`pandas.DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

**In addition** to the metadata described in the *core* schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md]('schema.md'), curators MUST annotate the following columns in the `obs` dataframe:

### array_col

<table><tbody>
    <tr>
      <th>Key</th>
      <td>array_col</td>
    </tr>
    <tr>
      <th>Annotator</th>
         <td>Curator MUST annotate if <code>assay_ontology_term_id</code> is  a descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0010961"><code>"EFO:0010961"</code></a> for <i>Visium Spatial Gene Expression</i> and <code>uns['spatial']['is_single']</code> is <code>True</code>; otherwise, this key MUST NOT be present.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>int</code>. This MUST be the value of the column coordinate for the corresponding spot from the <code>array_col</code> field in <code>tissue_positions_list.csv</code> or <code>tissue_positions.csv</code>. See <a href="https://www.10xgenomics.com/support/software/space-ranger/analysis/outputs/spatial-outputs">Space Ranger Spatial Outputs</a>.<br>
        <br>
          <table>
          <thead>
          <tr>
          <th>For Assay</th>
          <th>Value MUST be in<br>the range between</th>
          </tr>
          </thead>
          <tbody>
            <tr>
              <td><i>Visium Spatial Gene Expression V1</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022857"><code>EFO:0022857</code></a>]</td>
              <td><code>0</code> and <code>127</code></td>
           </tr> 
            <tr>
              <td><i>Visium CytAssist Spatial Gene Expression, 6.5mm</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022859"><code>EFO:0022859</code></a>]</td>
              <td><code>0</code> and <code>127</code></td>
           </tr>
            <tr>
              <td><i>Visium CytAssist Spatial Gene Expression, 11mm</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022860"><code>EFO:0022860</code></a>]</td>
              <td><code>0</code> and <code>223</code></td>
           </tr>
          </tbody></table>
        </td>
    </tr>
</tbody></table>
<br>

### array_row

<table><tbody>
    <tr>
      <th>Key</th>
      <td>array_row</td>
    </tr>
    <tr>
      <th>Annotator</th>
         <td>Curator MUST annotate if <code>assay_ontology_term_id</code> is a descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0010961"><code>"EFO:0010961"</code></a> for <i>Visium Spatial Gene Expression</i> and <code>uns['spatial']['is_single']</code> is <code>True</code>; otherwise, this key MUST NOT be present.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>int</code>. This MUST be value of the row coordinate for the corresponding spot from the <code>array_row</code> field in in <code>tissue_positions_list.csv</code> or <code>tissue_positions.csv</code>. See <a href="https://www.10xgenomics.com/support/software/space-ranger/analysis/outputs/spatial-outputs">Space Ranger Spatial Outputs</a>.<br>
        <br>
          <table>
          <thead>
          <tr>
          <th>For Assay</th>
          <th>Value MUST be in<br>the range between</th>
          </tr>
          </thead>
          <tbody>
            <tr>
              <td><i>Visium Spatial Gene Expression V1</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022857"><code>EFO:0022857</code></a>]</td>
              <td><code>0</code> and <code>77</code></td>
           </tr> 
            <tr>
              <td><i>Visium CytAssist Spatial Gene Expression, 6.5mm</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022859"><code>EFO:0022859</code></a>]</td>
              <td><code>0</code> and <code>77</code></td>
           </tr>
            <tr>
              <td><i>Visium CytAssist Spatial Gene Expression, 11mm</i> [<a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0022860"><code>EFO:0022860</code></a>]</td>
              <td><code>0</code> and <code>127</code></td>
           </tr>
          </tbody></table>
        </td>
    </tr>
</tbody></table>
<br>

### in_tissue

<table><tbody>
    <tr>
      <th>Key</th>
      <td>in_tissue</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Curator MUST annotate if <code>assay_ontology_term_id</code> is a descendant of <a href="https://www.ebi.ac.uk/ols4/ontologies/efo/classes?obo_id=EFO%3A0010961"><code>"EFO:0010961"</code></a> for <i>Visium Spatial Gene Expression</i> and <code>uns['spatial']['is_single']</code> is <code>True</code>; otherwise, this key MUST NOT be present.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>int</code>. This MUST be the value for the corresponding spot from the <code>in_tissue</code> field in <code>tissue_positions_list.csv</code> or <code>tissue_positions.csv</code> which is either <code>0</code> if the spot falls outside tissue or <code>1</code> if the spot falls inside tissue. See <a href="https://www.10xgenomics.com/support/software/space-ranger/analysis/outputs/spatial-outputs">Space Ranger Spatial Outputs</a>.
        </td>
    </tr>
</tbody></table>
<br>

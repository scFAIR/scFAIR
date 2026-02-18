# Schema

Contact: vincent.gardeux@epfl.ch

Document Status: _Drafting_

Version: 7.1.0_scfair

Current schema: **perturb**

## Schema split

The scFAIR schema is split into multiple part, to differentiate the metadata specific to certain modalities:
- The **core** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md]('schema.md') is the main schema for all types of single-cell data (scRNA-seq, scATAC-seq, perturbation, spatial, ...). It describes the core metadata between all modalities.
- The **spatial** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_spatial.md]('schema_spatial.md') describes the additional metadata that are specific to spatial datasets (Visium)
- This **perturb** schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema_perturb.md]('schema_perturb.md') describes the additional metadata that are specific to perturbation datasets (CRISPR screens, perturb-seq, ...)

## `obs` (Cell Metadata)

`obs` is a [`pandas.DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

**In addition** to the metadata described in the *core* schema [https://github.com/scFAIR/scFAIR/blob/main/schema/7.1.0/schema.md]('schema.md'), curators MUST annotate the following columns in the `obs` dataframe:

### genetic_perturbation_id

<table><tbody>
    <tr>
      <th>Key</th>
      <td>genetic_perturbation_id</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Curator MUST annotate if <code>uns['genetic_perturbations']</code> is present; otherwise this key MUST NOT be present.</td>
    </tr>
    <tr>
      <th>Value</th>
        <td>
          categorical with <code>str</code> categories. The corresponding <code>organism_ontology_term_id</code> MUST be one of: 
          <ul>
            <li>
              <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A7955"><code>"NCBITaxon:7955"</code></a> for <i>Danio rerio</i>
            </li>
            <li>
              <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A9606"><code>"NCBITaxon:9606"</code></a> for <i>Homo sapiens</i>
           </li>
            <li>
            <a href="https://www.ebi.ac.uk/ols4/ontologies/ncbitaxon/classes?obo_id=NCBITaxon%3A10090"><code>"NCBITaxon:10090"</code></a> for <i>Mus musculus</i>
           </li>
         </ul>
         The value MUST be either be <code>"na"</code> or one or more genetic perturbation identifiers in ascending lexical order separated by the delimiter <code>" || "</code> with no duplication of identifiers. Each identifier MUST match a <code>uns['genetic_perturbations'][<i>id</i>]</code>. If the corresponding value of <code>genetic_perturbation_strategy</code> is <code>"control"</code>, then the value of the role in <code>uns['genetic_perturbations'][<i>id</i>]['role']</code> for each matching <code>uns['genetic_perturbations'][<i>id</i>]</code> MUST be <code>"control"</code>.<br><br>All observations MUST NOT contain <code>"na"</code>.
        </td>
    </tr>
</tbody></table>
<br>

### genetic_perturbation_strategy

<table><tbody>
    <tr>
      <th>Key</th>
      <td>genetic_perturbation_strategy</td>
    </tr>
    <tr>
      <th>Annotator</th>
      <td>Curator MUST annotate if <code>obs['genetic_perturbation_id']</code> is present; otherwise, this key MUST NOT be present</td>
    </tr>
    <tr>
      <th>Value</th>
        <td><code>str</code>. If the corresponding value of <code>obs['genetic_perturbation_id']</code> is <code>"na"</code>, then the value MUST be <code>"no perturbations"</code>; otherwise, the value MUST be one of:
          <ul>
            <li><code>"control"</code></li>
            <li><code>"CRISPR activation screen"</code></li>
            <li><code>"CRISPR interference screen"</code></li>
            <li><code>"CRISPR knockout mutant"</code> describes F0 (founder generation) samples and does not include subsequent generations of homozygous mutants.</li> 
            <li><code>"CRISPR knockout screen"</code></li>
         </ul>
        </td>
    </tr>
</tbody></table>
<br>



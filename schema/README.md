# Metadata schemas compatible with scFAIR.

Of note, all schemas are forked from releases from [CZI schema](https://github.com/chanzuckerberg/single-cell-curation/tree/main/schema)
They are EXTENDING the CZI schemas, which means that all CZI schemas should be compatible with scFAIR schemas. However, this is not reciprocal.
In particular, scFAIR schemas:
- Allow for more species
- Add required metadata fields such as genome assembly
- ...

# Metadata schemas compatible with scFAIR.

Of note, all schemas are forked from releases from [CZI CELLxGENE schema](https://github.com/chanzuckerberg/single-cell-curation/tree/main/schema)
They are EXTENDING the CELLxGENE schemas, which means that all CELLxGENE schemas should be compatible with scFAIR schemas. However, this is not reciprocal.
In particular, scFAIR schemas:
- Allow for more species
- Add required metadata fields such as genome assembly
- ...

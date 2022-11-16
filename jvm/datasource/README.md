# Data Sources

https://howqueryengineswork.com/04-data-sources.html

Interface

- Have a schema
- Scan data out, only includes projection? What about predicate push down
    - Return value is Sequence, which is lazy and similar to java
      stream? https://stackoverflow.com/questions/35629159/kotlins-iterable-and-sequence-look-exactly-same-why-are-two-types-required

Sources

- CSV is using https://github.com/uniVocity/univocity-parsers same as spark
    - Infer schema is very basic ... without providing explicit schema, assume all columns are string
- In memory wraps list of records, return as sequence with mapping
- Parquet is still reading by row .. seems the implementation is broken ... reading by row seems to be a parquet-mr
  limitation?

Projection

- Columnar does not require construct new tuple like row based does, more memory and CPU efficient
- In memory source is just iterating batches and do convert lazily
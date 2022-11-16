# Type System

- https://howqueryengineswork.com/03-type-system.html

Wraps on Apache Arrow types

```text
// Apache Arrow
// https://mvnrepository.com/artifact/org.apache.arrow/arrow-memory
implementation 'org.apache.arrow:arrow-memory:10.0.0'
// https://mvnrepository.com/artifact/org.apache.arrow/arrow-vector
implementation 'org.apache.arrow:arrow-vector:10.0.0'
```

- Schema is list of field
- Field is name + type, type is using arrow vector directly
- Types are primitive types
    - [ ] What about complex type such as list and map, they can be modeled using primitive types though ...

`LiteralValueVector` return same value as offset is within the range because it is a constant for every row.

- RecordBatch is just a batch of records, kquery is using list of column vectors for a batch, using a list of tuple in
  row format is also doable (and less efficient in some use cases).
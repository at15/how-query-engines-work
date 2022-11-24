# Logical Plan & Expression

https://howqueryengineswork.com/05-logical-plan.html

- Logical Plan is projection, join etc, evaluation returns a new table
- Expression is variable, function, constant, evaluation returns a scalar value
    - [ ] What about COUNT(*), MAX(foo)?

## Expression

- `toField` is more like type of evaluation result

```kotlin
/**
 * Logical Expression for use in logical query plans. The logical expression provides information
 * needed during the planning phase such as the name and data type of the expression.
 */
interface LogicalExpr {

    /**
     * Return meta-data about the value that will be produced by this expression when evaluated
     * against a particular input.
     */
    fun toField(input: LogicalPlan): Field
}
```

Expressions are defined in Expressions.kt, multiple classes in one file one good thing about Kotlin

- Column name
- Literal, i.e. constant
- Binary, AND, OR
- Comparison, =, !=, <, >
- Math, +, -, *, /
- Aggregation, COUNT(*) ignores input type while MAX(foo) uses same type
    - Only works with function that has one parameter, e.g. percentile(a, 99) won't work in current logical plan

## Logical Plan

- Scan, leaf plan on a data source with (simple) projection
    - [ ] What is the `path` for? print?
- Projection, can apply expression of fields, not just selecting fields, e.g. `SELECT a + 2, b - 3`
- Selection, where, e.g. `SELECT a FROM foo WHERE a > 10`
- Aggregation, `SELECT department, COUNT(*) FROM people GROUP BY department`
- [ ] Join is in code but not mentioned in book
- [ ] No sort ...

## DataFrame

Just a fluent builder to avoid calling individual plan's constructor.

-
Spark https://github.com/apache/spark/blob/3c967f06e6c37360e53f9c7a5ecff95ae818e713/sql/core/src/main/scala/org/apache/spark/sql/Dataset.scala#L1715
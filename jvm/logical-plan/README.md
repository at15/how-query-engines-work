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

- [ ] join etc.
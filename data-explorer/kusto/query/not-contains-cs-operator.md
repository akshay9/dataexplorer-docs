---
title: The case-sensitive !contains_cs string operator - Azure Data Explorer
description: Learn how to use the !contains_cs string operator to filter data that doesn't include a case-sensitive string.
ms.reviewer: alexans
ms.topic: reference
ms.date: 12/26/2022
---

# !contains_cs operator

Filters a record set for data that doesn't include a case-sensitive string. `contains` searches for characters rather than [terms](datatypes-string-operators.md#what-is-a-term) of three or more characters. The query scans the values in the column, which is slower than looking up a term in a term index.

The following table provides a comparison of the `contains` operators:

|Operator   |Description   |Case-Sensitive  |Example (yields `true`)  |
|-----------|--------------|----------------|-------------------------|
|[`contains`](contains-operator.md) |RHS occurs as a subsequence of LHS |No |`"FabriKam" contains "BRik"`|
|[`!contains`](not-contains-operator.md) |RHS doesn't occur in LHS |No |`"Fabrikam" !contains "xyz"`|
|[`contains_cs`](contains-cs-operator.md) |RHS occurs as a subsequence of LHS |Yes |`"FabriKam" contains_cs "Kam"`|
|[`!contains_cs`](not-contains-cs-operator.md)   |RHS doesn't occur in LHS |Yes |`"Fabrikam" !contains_cs "Kam"`|

> [!NOTE]
> The following abbreviations are used in the above table:
>
> * RHS = right hand side of the expression
> * LHS = left hand side of the expression

For more information about other operators and to determine which operator is most appropriate for your query, see [datatype string operators](datatypes-string-operators.md).

## Performance tips

[!INCLUDE [performance-tip-note](../../includes/performance-tip-note.md)]

For faster results, use the case-sensitive version of an operator. For example, use `contains_cs` instead of `contains`.

If you're testing for the presence of a symbol or alphanumeric word that is bound by non-alphanumeric characters at the start or end of a field, for faster results use `has` or `in`. Also, `has` works faster than `contains`, `startswith`, or `endswith`, however it isn't as precise and could provide unwanted records.

## Syntax

### Case-sensitive syntax

*T* `|` `where` *Column* `!contains_cs` `(`*Expression*`)`

## Arguments

* *T* - The tabular input whose records are to be filtered.
* *Column* - The column to filter.
* *Expression* - Scalar or literal expression.

## Returns

Rows in *T* for which the predicate is `true`.

## Examples

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
StormEvents
    | summarize event_count=count() by State
    | where State !contains_cs "AS"
    | count
```

**Output**

|Count|
|-----|
|59|

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
StormEvents
    | summarize event_count=count() by State
    | where State !contains_cs "TEX"
    | where event_count > 3000
    | project State, event_count
```

**Output**

|State|event_count|
|-----|-----------|
|KANSAS|3,166|

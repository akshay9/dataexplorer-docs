---
title: The !between operator - Azure Data Explorer
description: This article describes the !between operator in Azure Data Explorer.
ms.reviewer: alexans
ms.topic: reference
ms.date: 10/23/2018
---
# !between operator

Matches the input that is outside the inclusive range.

```kusto
Table1 | where Num1 !between (1 .. 10)
Table1 | where Time !between (datetime(2017-01-01) .. datetime(2017-01-01))
```

`!between` can operate on any numeric, datetime, or timespan expression.
 
## Syntax

*T* `|` `where` *expr* `!between` `(`*leftRange*` .. `*rightRange*`)`   
 
If *expr* expression is datetime - another syntactic sugar syntax is provided:

*T* `|` `where` *expr* `!between` `(`*leftRangeDateTime*` .. `*rightRangeTimespan*`)`   

## Arguments

* *T* - The tabular input whose records are to be matched.
* *expr* - the expression to filter.
* *leftRange* - expression of the left range (inclusive).
* *rightRange* - expression of the right range (inclusive).

## Returns

Rows in *T* for which the predicate of (*expr* < *leftRange* or *expr* > *rightRange*) evaluates to `true`.

## Examples  

### Filter numeric values   

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
range x from 1 to 10 step 1
| where x !between (5 .. 9)
```

**Output**

|x|
|---|
|1|
|2|
|3|
|4|
|10|

### Filter datetime  

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
StormEvents
| where StartTime !between (datetime(2007-07-27) .. datetime(2007-07-30))
| count 
```

**Output**

|Count|
|---|
|58590|

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
StormEvents
| where StartTime !between (datetime(2007-07-27) .. 3d)
| count 
```

**Output**

|Count|
|---|
|58590|

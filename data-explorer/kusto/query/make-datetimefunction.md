---
title: make_datetime() - Azure Data Explorer
description: Learn how to use the make_datetime() function to create a datetime scalar value from the specified date and time.
ms.reviewer: alexans
ms.topic: reference
ms.date: 12/26/2022
---
# make_datetime()

Creates a [datetime](./scalar-data-types/datetime.md) scalar value from the specified date and time.

```kusto
make_datetime(2017,10,01,12,10) == datetime(2017-10-01 12:10)
```

## Syntax

`make_datetime(`*year*, *month*, *day*`)`

`make_datetime(`*year*, *month*, *day*, *hour*, *minute*`)`

`make_datetime(`*year*, *month*, *day*, *hour*, *minute*, *second*`)`

## Arguments

* *year*: year (an integer value, from 0 to 9999)
* *month*: month (an integer value, from 1 to 12)
* *day*: day (an integer value, from 1 to 28-31)
* *hour*: hour (an integer value, from 0 to 23)
* *minute*: minute (an integer value, from 0 to 59)
* *second*: second (a real value, from 0 to 59.9999999)

## Returns

If creation is successful, result will be a [datetime](./scalar-data-types/datetime.md) value, otherwise, result will be null.

## Example

```kusto
print year_month_day = make_datetime(2017,10,01)
```

**Output**

|year_month_day|
|---|
|2017-10-01 00:00:00.0000000|

```kusto
print year_month_day_hour_minute = make_datetime(2017,10,01,12,10)
```

**Output**

|year_month_day_hour_minute|
|---|
|2017-10-01 12:10:00.0000000|

```kusto
print year_month_day_hour_minute_second = make_datetime(2017,10,01,12,11,0.1234567)
```

**Output**

|year_month_day_hour_minute_second|
|---|
|2017-10-01 12:11:00.1234567|

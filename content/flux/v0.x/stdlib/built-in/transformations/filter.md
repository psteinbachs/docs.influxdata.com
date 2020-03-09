---
title: filter() function
description: The filter() function filters data based on conditions defined in a predicate
  function (fn).
aliases:
  - /flux/v0.x/functions/transformations/filter
  - /flux/v0.x/functions/built-in/transformations/filter/
menu:
  flux_0_x:
    name: filter
    parent: Transformations
    weight: 1
---

The `filter()` function filters data based on conditions defined in a predicate function ([`fn`](#fn)).
The output tables have the same schema as the corresponding input tables.

_**Function type:** Transformation_  
_**Output data type:** Object_

```js
filter(
  fn: (r) => r._measurement == "cpu",
  onEmpty: "drop"
)
```

## Parameters

### fn
A single argument predicate function that evaluates true or false.
Records are passed to the function.
Those that evaluate to true are included in the output tables.
Records that evaluate to _null_ or false are not included in the output tables.

_**Data type:** Function_

> Objects evaluated in `fn` functions are represented by `r`, short for "record" or "row".

{{% note %}}
Make sure `fn` parameter names match each specified parameter.
To learn why, see [Match parameter names](/flux/v0.x/language/data-model/#match-parameter-names).
{{% /note %}}

### onEmpty
Defines the behavior for empty tables.
Potential values are `keep` and `drop`.
Defaults to `drop`.

##### drop
Empty tables are dropped.

##### keep
Empty tables are output to the next transformation.

_**Data type:** String_

## Examples
```js
from(bucket:"telegraf/autogen")
  |> range(start:-1h)
  |> filter(fn: (r) =>
    r._measurement == "cpu" and
    r._field == "usage_system" and
    r.cpu == "cpu-total"
  )
```

<hr style="margin-top:4rem"/>

##### Related InfluxQL functions and statements:
[SELECT](/influxdb/latest/query_language/data_exploration/#the-basic-select-statement)
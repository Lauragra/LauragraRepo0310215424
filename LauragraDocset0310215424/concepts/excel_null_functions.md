# Excel null functions in Microsoft Graph

This topic provides examples of common Excel null functions that you can access via Microsoft Graph. 

## null input in 2-D array

`null` input inside a two-dimensional array (for values, number-format, formula) is ignored in the Range and Table resources. No update will take place to the intended target (cell) when `null` input is sent in values or number-format or formula grid of values.

For example, to only update specific parts of the Range, such as a cell's Number Format, and to retain the existing number-format on other parts of the Range, set the Number Format where needed and send `null` for the other cells.

In the following set request, only some parts of the Range Number Format are set while the existing Number Format on the remaining part is retained (by passing nulls).

```json
{
  "values" : [["Eurasia", "29.96", "0.25", "15-Feb" ]],
  "numberFormat" : [[null, null, null, "m/d/yyyy;@"]]
}
```

## null input for a property

`null` is not a valid single input for the entire property. For example, the following is not valid because the entire values cannot be set to null or ignored.

```json
{
"values":  null
}

```

The following is not valid either as null is not a valid color value.

```json
{
"color" :  null
}
```

## Null-Response

Representation of formatting properties that consists of non-uniform values results in the return of a null value in the response.

For example, a Range can consist of one or more cells. In cases where the individual cells contained in the Range specified don't have uniform formatting values, the range level representation will be undefined.

```json
{
  "size: : null,
  "color" : null
}
```


## Blank input and output

Blank values in update requests are treated as an instruction to clear or reset the respective property. A blank value is represented by two double quotation marks with no space in-between: `""`

Examples:

* For `values`, the range value is cleared out. This is the same as clearing the contents in the application.

* For `numberFormat`, the number format is set to `General`.

* For `formula` and `formulaLocale`, the formula values are cleared.


For read operations, expect to receive blank values if the contents of the cells are blanks. If the cell contains no data or value, the API returns a blank value. Blank value is represented by two double quotation marks with no space in-between: `""`

```json
{
  "values" : [["", "some", "data", "in", "other", "cells", ""]]
}
```

```json
{
  "formula" : [["", "", "=Rand()"]]
}
```

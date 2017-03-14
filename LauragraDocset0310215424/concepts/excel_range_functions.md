# Excel range functions in Microsoft Graph

This topic provides examples of common Excel range functions that you can access via Microsoft Graph. 

## Get Range 

Request
<!-- { "blockType": "ignored" } -->
```http
GET /{version}/me/drive/items/01CYZLFJDYBLIGAE7G5FE3I4VO2XP7BLU4/workbook/worksheets('test')/range(address='A1:B2')
authorization: Bearer {access-token} 
workbook-session-id: {session-id}
```

Response 

<!-- { "blockType": "ignored" } -->
```http
HTTP code: 200, OK
content-type: application/json;odata.metadata 

{
  "@odata.context": "https://graph.microsoft.com/{version}/$metadata#range",
  "@odata.type": "#microsoft.graph.range",
  "@odata.id": "/users('f6d92604-4b76-4b70-9a4c-93dfbcc054d5')/drive/items('01CYZLFJDYBLIGAE7G5FE3I4VO2XP7BLU4')/workbook/worksheets(%27%7B00000000-0001-0000-0300-000000000000%7D%27)/range(address=%27A1:B2%27)",
  "address": "test!A1:B2",
  "addressLocal": "test!A1:B2",
  "cellCount": 4,
  "columnCount": 2,
  "columnHidden": false,
  "columnIndex": 0,
  "formulas": [
    [
      "",
      ""
    ],
    [
      "",
      ""
    ]
  ],
  "formulasLocal": [
    [
      "",
      ""
    ],
    [
      "",
      ""
    ]
  ],
  "formulasR1C1": [
    [
      "",
      ""
    ],
    [
      "",
      ""
    ]
  ],
  "hidden": false,
  "numberFormat": [
    [
      "General",
      "General"
    ],
    [
      "General",
      "General"
    ]
  ],
  "rowCount": 2,
  "rowHidden": false,
  "rowIndex": 0,
  "text": [
    [
      "",
      ""
    ],
    [
      "",
      ""
    ]
  ],
  "values": [
    [
      "",
      ""
    ],
    [
      "",
      ""
    ]
  ],
  "valueTypes": [
    [
      "Empty",
      "Empty"
    ],
    [
      "Empty",
      "Empty"
    ]
  ]
}
```

## Range update 

<!-- { "blockType": "ignored" } -->
```http
PATCH /{version}/me/drive/items/01CYZLFJDYBLIGAE7G5FE3I4VO2XP7BLU4/workbook/worksheets('test')/range(address='test!A1:B2')
authorization: Bearer {access-token} 
workbook-session-id: {session-id}

{ "values": [ [ "Test", "Value" ], [ "For", "Update" ] ] }
```

<!-- { "blockType": "ignored" } -->
```http
HTTP code: 200, OK
content-type: application/json;odata.metadata

{
  "@odata.context": "https://graph.microsoft.com/{version}/$metadata#range",
  "@odata.type": "#microsoft.graph.range",
  "@odata.id": "/users('f6d92604-4b76-4b70-9a4c-93dfbcc054d5')/drive/items('01CYZLFJDYBLIGAE7G5FE3I4VO2XP7BLU4')/workbook/worksheets(%27%7B00000000-0001-0000-0300-000000000000%7D%27)/range(address=%27test!A1:B2%27)",
  "address": "test!A1:B2",
  "addressLocal": "test!A1:B2",
  "cellCount": 4,
  "columnCount": 2,
  "columnHidden": false,
  "columnIndex": 0,
  "formulas": [
    [
      "Test",
      "Value"
    ],
    [
      "For",
      "Update"
    ]
  ],
  "formulasLocal": [
    [
      "Test",
      "Value"
    ],
    [
      "For",
      "Update"
    ]
  ],
  "formulasR1C1": [
    [
      "Test",
      "Value"
    ],
    [
      "For",
      "Update"
    ]
  ],
  "hidden": false,
  "numberFormat": [
    [
      "General",
      "General"
    ],
    [
      "General",
      "General"
    ]
  ],
  "rowCount": 2,
  "rowHidden": false,
  "rowIndex": 0,
  "text": [
    [
      "Test",
      "Value"
    ],
    [
      "For",
      "Update"
    ]
  ],
  "values": [
    [
      "Test",
      "Value"
    ],
    [
      "For",
      "Update"
    ]
  ],
  "valueTypes": [
    [
      "String",
      "String"
    ],
    [
      "String",
      "String"
    ]
  ]
}
```

## Range sort
Request
<!-- { "blockType": "ignored" } -->
```http
POST /{version}/me/drive/items/01CYZLFJGUJ7JHBSZDFZFL25KSZGQTVAUN/workbook/worksheets('Sheet15799')/usedRange/sort/apply
authorization: Bearer {access-token} 
workbook-session-id: {session-id}

{
"fields" : [
  { "key": 0,
   "ascending": true
  }
]
}
```

Response
<!-- { "blockType": "ignored" } -->
```http
HTTP code: 204, No Content
```

## Unbounded Range

### Read

Unbounded Range address contains only column or row identifiers and unspecified row identifier or column identifiers (respectively), such as:

* `C:C`, `A:F`, `A:XFD` (contains unspecified rows)
* `2:2`, `1:4`, `1:1048546` (contains unspecified columns)

When the API makes a request to retrieve an unbounded Range (`getRange('C:C')`), the response returned contains `null` for cell-level properties such as `values`, `text`, `numberFormat`, or `formula`. Other Range properties such as `address` or `cellCount` will reflect the unbounded range.

### Write

Setting cell level properties (such as values, numberFormat, etc.) on unbounded Range is **not allowed** because the input request might be too large to handle.

For example, the following is not a valid update request because the requested range is unbounded.

<!-- { "blockType": "ignored" } -->
```http
PATCH /workbook/worksheets('Sheet1')/range(address="A:B")

{
  "values" : "Due Date"
}
```

When an update operation is attempted on such a Range, the API will return an error.


## Large Range

Large Range implies a Range of a size that is too large for a single API call. Many factors such as number of cells, values, numberFormat, and formulas contained in the range can make the response so large that it becomes unsuitable for API interaction. The API makes a best attempt to return or write to the requested data. However, the large size involved might result in an API error condition because of the large resource utilization.

To avoid this, we recommend that you read or write for large Range in multiple smaller range sizes.


## Single input copy

To support updating a range with the same values or number-format or applying same formula across a range, the following convention is used in the set API. In Excel, this behavior is similar to inputting values or formulas to a range in the CTRL+Enter mode.

The API will look for a *single cell value* and, if the target range dimension doesn't match the input range dimension, it will apply the update to the entire range in the CTRL+Enter model with the value or formula provided in the request.

### Examples

The following request updates the selected range with the text of "Sample text". Note that Range has 200 cells, whereas the provided input only has 1 cell value.

<!-- { "blockType": "ignored" } -->
```http
PATCH /workbook/worksheets('Sheet1')/range(address="A1:B00")

{
  "values" : "Sample text"
}
```
# Get TableRow

Retrieve the properties and relationships of tablerow object.
## Prerequisites
The following **scopes** are required to execute this API: 
## HTTP request
<!-- { "blockType": "ignored" } -->
```http
GET /workbook/tables(<id|name>)/rows(<index>)
GET /workbook/worksheets(<id|name>)/tables(<id|name>)/rows(<index>)
```
## Optional query parameters
This method supports the [OData Query Parameters](http://graph.microsoft.io/docs/overview/query_parameters) to help customize the response.

## Request headers
| Name      |Description|
|:----------|:----------|
| Authorization  | Bearer <code>|


## Request body
Do not supply a request body for this method.
## Response
If successful, this method returns a `200 OK` response code and [TableRow](../resources/tablerow.md) object in the response body.
## Example
##### Request
Here is an example of the request.
<!-- {
  "blockType": "request",
  "name": "get_tablerow"
}-->
```http
GET https://graph.microsoft.com/v1.0/me/drive/items/<id>/workbook/tables(<id|name>)/rows(<index>)
```
##### Response
Here is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.tableRow"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json
Content-length: 45

{
  "index": 99,
  "values": "values-value"
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Get TableRow",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
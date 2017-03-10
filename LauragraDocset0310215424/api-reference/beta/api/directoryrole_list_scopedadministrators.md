# List scopedAdministrators for a directory role

Retrieve a list of [scopedRoleMembership](../resources/scopedrolemembership.md) objects for a directory role.
## Prerequisites
The following **scopes** are required to execute this API: *Directory.Read.All* or *Directory.ReadWrite.All* or *Directory.AccessAsUser.All*.
## HTTP request
<!-- { "blockType": "ignored" } -->
```http
GET /directoryRoles/<id>/scopedAdministrators
```
## Optional query parameters
This method supports the [OData Query Parameters](http://graph.microsoft.io/docs/overview/query_parameters) to help customize the response.

## Request headers
| Name      |Description|
|:----------|:----------|
| Authorization  | Bearer <token>. Required.|

## Request body
Do not supply a request body for this method.
## Response
If successful, this method returns a `200 OK` response code and collection of [scopedRoleMembership](../resources/scopedrolemembership.md) objects in the response body.
## Example
##### Request
Here is an example of the request.
<!-- {
  "blockType": "request",
  "name": "get_scopedadministrators_directoryrole"
}-->
```http
GET https://graph.microsoft.com/beta/directoryRoles/<id>/scopedAdministrators
```
##### Response
Here is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.scopedrolemembership",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json
Content-length: 307

{
  "value": [
    {
      "roleId": "roleId-value",
      "administrativeUnitId": "administrativeUnitId-value",
      "roleMemberInfo": {
        "id": "id-value",
        "displayName": "displayName-value",
        "userPrincipalName": "userPrincipalName-value"
      },
      "id": "id-value"
    }
  ]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "List scopedAdministrators",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
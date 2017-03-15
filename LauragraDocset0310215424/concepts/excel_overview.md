# Working with Excel in Microsoft Graph

You can use Microsoft Graph to allow web and mobile applications to read and modify Excel workbooks stored in OneDrive, SharePoint, or other supported storage platforms. The `Workbook` (or Excel file) resource contains all the other Excel resources through relationships. You can access a workbook through the [Drive API](drive.md) by identifying the location of the file in the URL. For example:

`https://graph.microsoft.com/{version}/me/drive/items/{id}/workbook/`  
`https://graph.microsoft.com/{version}/me/drive/root:/{item-path}:/workbook/`  

You can access a set of Excel objects (such as Table, Range, or Chart) by using standard REST APIs to perform  create, read, update, and delete (CRUD) operations on the workbook. For example, 
`https://graph.microsoft.com/{version}/me/drive/items/{id}/workbook/`  
returns a collection of worksheet objects that are part of the workbook.    


## Authorization and scopes

You can use the [Azure AD v.20 endpoint](https://graph.microsoft.io/en-us/docs/authorization/converged_auth) to authenticate Excel APIs. All APIs require the `Authorization: Bearer {access-token}` HTTP header.   
  
One of the following [permission scopes](https://graph.microsoft.io/en-us/docs/authorization/permission_scopes) is required to use the Excel resource:

* Files.Read 
* Files.ReadWrite


## Sessions and persistence

Excel APIs can be called in one of two modes: 

1. Persistent session - All changes made to the workbook are persisted (saved). This is the usual mode of operation. 
2. Non-persistent session - Changes made by the API are not saved to the source location. Instead, the Excel backend server keeps a temporary copy of the file that reflects the changes made during that particular API session. When the Excel session expires, the changes are lost. This mode is useful for apps that need to do analysis or obtain the results of a calculation or a chart image, but not affect the document state.   

To represent the session in the API, use the `workbook-session-id: {session-id}` header. 

>**Note:** The session header is not required for an Excel API to work. However, we recommend that you use the session header to improve performance. If you don't use a session header, changes made during the API call _are_ persisted to the file.  

### API call to get a session 

#### Request 

Pass a JSON object by setting the `persistchanges` value to `true` or `false`. 

<!-- { "blockType": "ignored" } -->
```http
POST /{version}/me/drive/items/01CYZLFJGUJ7JHBSZDFZFL25KSZGQTVAUN/workbook/createSession
content-type: Application/Json 
authorization: Bearer {access-token}

{ "persistChanges": true }
```

When the value of `persistChanges` is set to `false`, a non-persistent session id is returned.  


#### Response

<!-- { "blockType": "ignored" } -->
```http
HTTP code: 201, Created
content-type: application/json;odata.metadata 

{
  "@odata.context": "https://graph.microsoft.com/{version}/$metadata#microsoft.graph.sessionInfo",
  "id": "{session-id}",
  "persistChanges": true
}
```

#### Usage 

The session ID returned from the previous call is passed as a header on subsequent API requests in  
`workbook-session-id` HTTP header. 

<!-- { "blockType": "ignored" } -->
```http
GET /{version}/me/drive/items/01CYZLFJGUJ7JHBSZDFZFL25KSZGQTVAUN/workbook/worksheets
authorization: Bearer {access-token} 
workbook-session-id: {session-id}
```

## Error information 

Errors are returned with an HTTP error code and an error object. An error `code` and `message` explain the reason for the error.
 
The following is an example.

<!-- { "blockType": "ignored" } -->
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": {
    "code": "ItemAlreadyExists",
    "message": "A resource with the same name or identifier already exists.",
    "innerError": {
      "request-id": "214ca7ea-9ea4-442e-9c67-71fdda0a559c",
      "date": "2016-07-28T03:56:09"
    }
  }
}
```


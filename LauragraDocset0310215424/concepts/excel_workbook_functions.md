# Excel range and workbook functions in Microsoft Graph

This topic provides examples of common Excel range and workbook functions that you can access via Microsoft Graph. You can access the workbook functions through a collection of functions included in the /Functions resource. 

<!-- LG: Where is the Functions resource? We should link to this.
-->
#### Request
<!-- { "blockType": "ignored" } -->
```http
POST https://graph.microsoft.com/v1.0/me/drive/root:/book1.xlsx:/workbook/functions/pmt
content-type: Application/Json 
authorization: Bearer {access-token} 
workbook-session-id: {session-id}

{
    "rate": 4.5,
    "nper": 12,
    "pv": -1250
}
```


#### Response 

<!-- { "blockType": "ignored" } -->
```http 
HTTP code: 200, OK
content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#workbookFunctionResult",
    "@odata.type": "#microsoft.graph.workbookFunctionResult",
    "@odata.id": "/users('f6d92604-4b76-4b70-9a4c-93dfbcc054d5')/drive/root/workbook/functions/pmt()",
    "error": null,
    "value": 5625.00000734125
}
```
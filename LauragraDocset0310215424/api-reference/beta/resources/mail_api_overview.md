# Using the Microsoft Graph API to integrate with Outlook mail

Microsoft Graph lets your app obtain authorized access to a user's Outlook mail data in a personal or organization account. 
With the [appropriate delegated or application permissions](../../../authorization/permission_scopes.md), your app can access the mail data of 
the signed-in user, or any user in a tenant. The mail data can be in the cloud on Exchange Online as part of Office 365, or on 
Exchange on-premises in a [hybrid deployment](../../../concepts/hybrid_rest_support.md).

## Using the mail REST API
Mail API requests are performed on behalf of a [user](../resources/user.md), identifiable by the user's **id** property (a unique GUID), 
or the `me` shortcut alias for the signed-in user.

Email messages are represented by the [message](../resources/message.md) resource and organized in a [mailFolder](../resources/mailfolder.md).
Messages and mail folders are identified by their **id** property obtainable from `GET` operations. 

>**Note** In general, do not assume **message** and **mailfolder** IDs are unique and immutable within a mailbox. They may change after certain 
actions such as copy, move, or send. 

To reference some mail folders in a user's mailbox, you can use well-known folder names such as `Inbox`, `Drafts`, `SentItems`, `DeletedItems`. 
As an example, you can get messages in the Outlook **Sent Items** folder as shown below, without first getting the folder ID:
```
GET /me/mailFolders('SentItems')/messages?$select=sender,subject
```

## Common use cases 

The **message** resource exposes properties such as **categories**, **conversationId**, **flag**, and **importance** that correspond to features 
available in the user interface, allowing apps to automate or integrate with the built-in Outlook user experience. 

Microsoft Graph API also provides methods and actions that support common use cases involving messages, as listed below. 

| Use cases		   | REST resources	| See also |
|:---------------|:--------|:----------|
| _**User-centric actions**_ | | |
| Draft, read, reply, forward, send, update, or delete messages | [message](../resources/message.md) | [Methods of message](../resources/message.md#methods) |
| Delegate another user to send messages on behalf of the mailbox owner | [message](../resources/message.md) | [Setting the from and sender properties](../resources/message.md#setting-the-from-and-sender-properties) |
| Let user view more important messages first | [inferenceClassificationOverride](../resources/inferenceClassificationOverride.md) | [Focused Inbox](../resources/manage_focused_inbox.md) |
| Add, get, or delete attachments of a message | [attachment](../resources/attachment.md), <br> [fileAttachment](../resources/fileattachment.md), <br> [itemAttachment](../resources/itemattachment.md), <br> [referenceAttachment](../resources/referenceattachment.md), <br> [message](../resources/message.md) | [Methods of attachment](../resources/attachment.md#methods) |
| Get or update a user's automatic reply, locale or time zone in mailbox settings | [mailboxSettings](../resources/mailboxsettings.md), <br> [automaticRepliesSetting](../resources/automaticrepliessetting.md), <br> [localeInfo](../resources/localeinfo.md) | [Get user's mailbox settings](../api/user_get_mailboxsettings.md), <br> [Update user's mailbox settings](../api/user_update_mailboxsettings.md) |
| Let user see MailTips about other recipients' special status, such as out-of-office (preview) | [user (preview)](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/resources/user.md), <br> [mailTips (preview)](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/resources/mailtips.md) | [Get MailTips](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/api/user_getmailtips.md) |
| Alert user when mentioned in other messages (preview) | [mention (preview)](../resources/mention.md) | [Get details of @-mentions in a message](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/api/message_get.md#request-2) |
| Unsubscribe user from an email distribution list (preview) | [message (preview)](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/resources/message.md) | [Unsubscribe](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/api/message_unsubscribe.md) |
| _**Mail and folder management**_ | | |
| Organize messages in a mail folder hierarchy | [mailFolder](../resources/mailfolder.md)  | [Methods of mailFolder](../resources/mailfolder.md#methods) |
| Search and filter messages | [message](../resources/message.md) | [Query parameters](../../../overview/query_parameters.md)  |
| Get notified of changes to messages in a folder | [subscription](../resources/subscription.md) | [Working with webhooks in Microsoft Graph](../resources/webhooks.md) |
| Synchronize messages or mail folder hierarchy (preview) | [message (preview)](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/resources/message.md) | [Get incremental changes to messages in a folder](../../../concepts/delta_query_messages.md) |
| _**App development**_ | | |
| Add custom app data to a message by using extensions | [openTypeExtension](../resources/opentypeextension.md), <br> [schemaExtension (preview)](https://developer.microsoft.com/en-us/graph/docs/api-reference/beta/resources/schemaextension.md) | [Add custom data to resources using extensions](../../../concepts/extensibility_overview.md) |
| Access custom data for under-exposed Outlook MAPI properties | [singleValueLegacyExtendedProperty](../resources/singlevaluelegacyextendedproperty.md), <br> [multiValueLegacyExtendedProperty](../resources/multivaluelegacyextendedproperty.md) | [Outlook extended properties overview](../resources/extended-properties-overview.md) |




## Next steps
The mail API can open up new ways for you to engage with users. 

Drill down on the [methods](../resources/message.md#methods), [properties](../resources/message.md#properties), and [relationships](../resources/message.md#relationships) 
of the [message](../resources/message.md) and [mailFolder](../resources/mailfolder.md) resources.

[Try](https://developer.microsoft.com/en-us/graph/graph-explorer) the API in the Graph Explorer.

Need more ideas? [See how some of our partners are using Microsoft Graph.](https://developer.microsoft.com/en-us/graph/graph/examples#partners)



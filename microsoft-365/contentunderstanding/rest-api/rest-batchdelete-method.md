---
title: BatchDelete
ms.author: chucked
author: chuckedmonson
manager: pamgreen
ms.reviewer: ssquires
audience: admin
ms.topic: reference
ms.prod: microsoft-365-enterprise
search.appverid: 
ms.collection: m365initiative-syntex
localization_priority: Priority
description: Use REST API to remove an applied document understanding model from one or more libraries.
---

# BatchDelete

Removes an applied document understanding model from one or more libraries. Note that a model must be removed from all libraries before it can be deleted (see [example](rest-batchdelete-method.md#examples)).

## HTTP request

```HTTP
POST /_api/machinelearning/publications/batchdelete HTTP/1.1
```

## URI parameters

None

## Request headers

| Header | Value |
|--------|-------|
|Accept|application/json;odata=verbose|
|Content-Type|application/json;odata=verbose;charset=utf-8|
|x-requestdigest|The appropriate digest for current site.|

## Request body

| Name | Required | Type | Description |
|--------|-------|--------|------------|
|ModelUniqueId|yes|string|The unique ID of the model file.|
TargetSiteUrl|yes|string|The full URL of the target library site.|
TargetWebServerRelativeUrl|yes|string|The server relative URL of the web for the target library.|
TargetLibraryServerRelativeUrl|yes|string|The server relative URL of the target library.|
ViewOption|no|string|Specifies whether to set new model view as the library default.|

## Response

| Name   | Type  | Description|
|--------|-------|------------|
|200 OK| |Success|


## Examples

### Remove a model from the contracts document library in the repository site

In this sample, the ID of the Contoso Contract document understanding model is `7645e69d-21fb-4a24-a17a-9bdfa7cb63dc`.

#### Sample request

```HTTP
{
	"__metadata": {
		"type": "Microsoft.Office.Server.ContentCenter.SPMachineLearningPublicationsEntityData"
	},
	"Publications": {
		"results": [
			{
				"ModelUniqueId": "7645e69d-21fb-4a24-a17a-9bdfa7cb63dc",
				"TargetSiteUrl": "https://contoso.sharepoint.com/sites/repository/",
				"TargetWebServerRelativeUrl": "/sites/repository",
				"TargetLibraryServerRelativeUrl": "/sites/repository/contracts",
				"ViewOption": "NewViewAsDefault"
			}
		]
	}
}
```


#### Sample response

In the response, TotalFailures and TotalSuccesses refer to the number of failures and successes of the model being applies to the specified libraries.

**Status code:** 200

```JSON
{
	"Details": [
		{
			"ErrorMessage": null,
			"Publication": {
				"ModelUniqueId": "7645e69d-21fb-4a24-a17a-9bdfa7cb63dc",
				"TargetSiteUrl": "https://contoso.sharepoint.com/sites/repository/",
				"TargetWebServerRelativeUrl": "/sites/repository",
				"TargetLibraryServerRelativeUrl": "/sites/repository/contracts",
				"ViewOption": "NewViewAsDefault"
			},
			"StatusCode": 200
		}
	],
	"TotalFailures": 0,
	"TotalSuccesses": 1
}
```

## See also

[Syntex document understanding model REST API](syntex-model-rest-api.md)

---
title: InfiniTweak API Reference


toc_footers:


search: true
---

# Introduction

Welcome to the InfiniTweak API !

`API_VERSION = 0.1`

## Response Structure


> Successful query without response 

```json
{
	"API" : <STR:API_VERSION>,
	"SUCCESSFUL" : TRUE
}
```

> Successful query with result 

```json
{
	"API" : <STR:API_VERSION>,
	"SUCCESSFUL" : TRUE,
	"RESULT" : <OBJ:RESULT>
}
```



> Unsuccessful action

```json
{
	"API" : <STR:API_VERSION>,
	"RESULT" : FALSE,
	"REASON" : <STR:ERROR>
}
```



### Status Codes

Code | Meaning | Reason
--------- | ------- | -----------
`200` | `Success` | 

## Callback Structure

# REST API Requests

## Engine : Init

> No result

> Error Code 

Create the I/O devices.

### HTTP Request

`GET http://InfiniTweak/api/engine/init`


## Engine : Start


> Result

```
None
```

> Errors
 
 
Code | Meaning | Reason
--------- | ------- | -----------
`200` | `Success` | 


Start the audio rendering process

### HTTP Request

`GET http://InfiniTweak/api/engine/start`

## Engine : Pause


> The result if it works : 

```json
{
	
}
```

Pause the audio rendering process

### HTTP Request

`GET http://InfiniTweak/api/engine/pause`

## Engine : Close


> The result if it works : 

```json
{
	
}
```

Stop the engine and remove all the I/O devices.

### HTTP Request

`GET http://InfiniTweak/api/engine/close`




## Files : Plugins


> The result if it works : 

```json
{
	
}
```

Get all the plugins located in the device drive.

### HTTP Request

`GET http://InfiniTweak/api/files/plugins`



## Plugin : Add 


> The result if it works : 

```json
{
	
}
```

Load and add a plugin to the patchbay

### HTTP Request

`POST http://InfiniTweak/api/plugins`

#### Query Parameters

##### Body

Parameter | Type | Description
--------- | ------- | -----------
`build` | `Int` | 
`type` | `Int` | 
`filename` | `Str` | 
`label` | `Str` |
`uniqueId` | `Int`

## Plugin : Remove 


> The result if it works : 

```json
{
	
}
```

Remove a plugin from the patchbay 

### HTTP Request

`DELETE http://InfiniTweak/api/plugins/<pluginId>`

#### Query Parameters




Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 


## Plugin : Info


> The result if it works : 

```json
{
	
}
```

Get info on a plugin

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>`

#### Query Parameters


Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | Int | 

## Plugin : Set parameter value


> The result if it works : 

```json
{
	
}
```


### HTTP Request

`PUT http://InfiniTweak/api/plugins/<pluginId>/<parameter>`

#### Query Parameters

##### URL

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 
`parameter` | <ul><li>`active` <li> `volume` <li> `<Int:parameterId>`</ul> 

##### BODY

Parameter | Type | Description
--------- | ------- | -----------
`value` | `Int` | 
## Plugin : Show UI


> The result if it works : 

```json
{
	
}
```

Show a plugin's UI

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>/UI`

#### Query Parameters


Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 


## Patchbay : Connect


> The result if it works : 

```json
{
	
}
```

Connect two devices/plugins

### HTTP Request

`POST http://InfiniTweak/api/patchbay/connections`

#### Query Parameters


Parameter | Type | Description
--------- | ------- | -----------
`clientIdA` | `Int` | 
`portIdA` | `Int`
`clientIdB` | `Int`
`portIdB` | `Int`



## Patchbay : Disconnect


> The result if it works : 

```json
{
	
}
```

Remove a connection between two devices/plugins

### HTTP Request

`DELETE http://InfiniTweak/api/patchbay/connections`

#### Query Parameters


Parameter | Type | Description
--------- | ------- | -----------
`connectionId`| `Int` | 










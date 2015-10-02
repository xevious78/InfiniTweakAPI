---
title: InfiniTweak API Reference



search: true
---

# Introduction

Welcome to the InfiniTweak API !

`API_VERSION = 0.1`

## Response Structure


> Successful query without result 

```json
{
	"API" : <STR:API_VERSION>,
	"SUCCESSFUL" : true
}
```

> Successful query with result 

```json
{
	"API" : <STR:API_VERSION>,
	"SUCCESSFUL" : true,
	"RESULT" : <OBJ:RESULT>
}
```


> Unsuccessful action

```json
{
	"API" : <STR:API_VERSION>,
	"RESULT" : false,
	"REASON" : <STR:ERROR>
}
```



### Status Codes

Code | Meaning | Reason
--------- | ------- | -----------
`200` | `Success` | 

## Callback Structure


> Callback Structure without details

```json
{
	"API" : <STR:API_VERSION>,
	"CALLBACK" : <STR:CALLBACK_MESSAGE>
}
```

> Callback Structure with details

```json
{
	"API" : <STR:API_VERSION>,
	"CALLBACK" : <STR:CALLBACK_MESSAGE>,
	"DETAILS" : <OBJ:DETAILS>
}
```

# REST API Requests

## Engine : Init

Create the I/O devices.

### HTTP Request

`GET http://InfiniTweak/api/engine/init`

### Result

None

### Error


## Engine : Start


Start the audio rendering process

### HTTP Request

`GET http://InfiniTweak/api/engine/start`

### Result

None

### Error

Error | Reason
--------- | ------- 
`ENGINE_CLOSED` | The engine is closed

## Engine : Pause


Pause the audio rendering process

### HTTP Request

`GET http://InfiniTweak/api/engine/pause`

### Result

None

### Error

Error | Reason
--------- | ------- 
`ENGINE_CLOSED` | The engine is closed




## Engine : Close

<aside class="warning">Doesn't work</aside>

Stop the engine and remove all the I/O devices.

### HTTP Request

`GET http://InfiniTweak/api/engine/close`

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Files : Plugins



> Result

```json
[
    {
      "midi.ins": 0,
      "type": 1,
      "name": "Bypass",
      "audio.ins": 1,
      "parameters.outs": 0,
      "filename": "",
      "API": 6,
      "midi.outs": 0,
      "build": 2,
      "uniqueId": 0,
      "audio.outs": 1,
      "label": "bypass",
      "parameters.ins": 0,
      "maker": "falkTX",
      "hints": 2
    }
]
```



Get all the plugins located in the device drive.

### HTTP Request

`GET http://InfiniTweak/api/files/plugins`

### Result

Parameter | Type | Description
--------- | ------- | -----------
`midi.ins` | `Int` | 
`type` | `Int` | 
`name` | `Str` | 
`audio.ins` | `Int` |
`parameters.out` | `Int` |
`filename` | `Str` |
`API` | `Int` |
`midi.outs` | `Int` |
`build` | `Int` |
`uniqueId` | `Int` |
`audio.outs` | `Int` |
`label` | `Str` |
`parameters.ins` | `Int` |
`maker` | `Str` |
`hints` | `Int` |

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Add 


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

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Remove 

Remove a plugin from the patchbay 

### HTTP Request

`DELETE http://InfiniTweak/api/plugins/<pluginId>`

#### URL


Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Plugin : Info


Get info on a plugin

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>`

#### Query Parameters

##### URL

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | Int | 

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Set parameter value

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

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Show UI


Show a plugin's UI

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>/UI`

#### Query Parameters


##### URL

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 


### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Patchbay : Connect


Connect two devices/plugins

### HTTP Request

`POST http://InfiniTweak/api/patchbay/connections`

#### Query Parameters

##### BODY


Parameter | Type | Description
--------- | ------- | -----------
`clientIdA` | `Int` | 
`portIdA` | `Int`
`clientIdB` | `Int`
`portIdB` | `Int`

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Patchbay : Disconnect




Remove a connection between two devices/plugins

### HTTP Request

`DELETE http://InfiniTweak/api/patchbay/connections`

#### Query Parameters

##### BODY

Parameter | Type | Description
--------- | ------- | -----------
`connectionId`| `Int` | 


### Results

None

### Errors

Error | Reason 
--------- | ------- 
`UNKNOWN_ERROR` |  | 






# WebSocket Callback



## Plugin : Added

### Callback Message
```
PLUGIN_ADDED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`pluginId`| `Int` | 
`pluginName`| `Int` | 



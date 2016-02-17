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

## WebSocket RESP Api Request Structure

> Request

```json
{
	"METHOD" : <STR:METHOD>,
	"URI" : <STR:URI>,
	"DATA" : <OBJ:DATA>
}
```

> Example

```json
{
	"METHOD" : "PUT",
	"URI" : "/api/plugins/0/parameters/1",
	"DATA" : 
		{
			"value" : 5.5
		}
}
```

# REST API Requests

## Engine : Is Running ?

Check if the engine is running

### HTTP Request

`GET http://InfiniTweak/api/engine/`

### Result

#### WebSocket Callback

`ENGINE_INITIALIZED` <br />
`PATCHBAY_CLIENT_ADDED` : I/O devices client
<br /> 
`PATCHBAY_PORT_ADDED` : I/O devices client port

## Engine : Init

Create the I/O devices.

### HTTP Request

`GET http://InfiniTweak/api/engine/init`

### Result

#### WebSocket Callback

`ENGINE_INITIALIZED` <br />
`PATCHBAY_CLIENT_ADDED` : I/O devices client
<br /> 
`PATCHBAY_PORT_ADDED` : I/O devices client port


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

Parameter | Type | Description
--------- | ------- | -----------
`value` | `Bool` | 



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

#### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
`build` | `Int` | 
`type` | `Int` | 
`filename` | `Str` | 
`label` | `Str` |
`uniqueId` | `Int`

### Result

#### WebSocket Callback

`PLUGIN_ADDED` <br />
`PATCHBAY_CLIENT_ADDED` <br /> 

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Remove All Plugins

Remove all plugins from the patchbay. 

### HTTP Request

`DELETE http://InfiniTweak/api/plugins`


### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Plugin : Remove 


Remove a plugin from the patchbay. All the `pluginId` are then reassigned so that there is no gap in the id count.

### HTTP Request

`DELETE http://InfiniTweak/api/plugins/<pluginId>`

#### URL Parameters


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

#### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | Int | 

### Result


Parameter | Type | Description
--------- | ------- | -----------
`info` | `Obj` | 
`parameterCount` | `Obj` | 
`midiPortCount` | `Obj` | 
`audioPortCount` | `Obj` |
`programCount` | `Int` |
`currentProgram` | `Int` | <ul><li>`-1` : No program</ul>

<br />


`info`

Parameter | Type | Description
--------- | ------- | -----------
`category` | `Int` | 
`name` | `Str` | 
`copyright` | `Str` | 
`optionsEnabled` | `Int` |
`filename` | `Str` |
`iconName` | `Str` | 
`uniqueId` | `Int` | 
`optionsAvailable` | `Int` | 
`label` | `Str` | 
`type` | `Int` | 
`maker` | `Str` | 
`hints` | `Int` | 

<br />


`parameterCount`

Parameter | Type | Description
--------- | ------- | -----------
`outs` | `Int` | 
`ins` | `Int` | 

<br />


`midiPortCount`

Parameter | Type | Description
--------- | ------- | -----------
`outs` | `Int` | 
`ins` | `Int` | 

<br />

`audioPortCount`

Parameter | Type | Description
--------- | ------- | -----------
`outs` | `Int` | 
`ins` | `Int` | 



### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : All Plugin Infos

Get info on all plugins currently in the patchbay

### HTTP Request

`GET http://InfiniTweak/api/plugins/`



### Result


Parameter | Type | Description
--------- | ------- | -----------
`result` | `Array of PluginInfo` | See *Plugin : Info*



## Plugin : Get parameter info

<aside class="warning">Cannot get anything except a parameterId (no volume, active, ...)</aside>


### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>/parameters/<parameter>`


#### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 
`parameter` | <ul>`<Int:parameterId>`</ul> 


### Result

Parameter | Type | Description
--------- | ------- | -----------
`info` | `Obj` | 
`ranges` | `Obj` | 
`currentValue` | `Int` | 
`defaultValue` | `Int` |
`internalValue` | `Int` |
`currentValue` | `Int` | 
<br />

`info`

Parameter | Type | Description
--------- | ------- | -----------
`name` | `Str` | 
`symbol` | `Str` | 
`unit` | `Str` |
`scalePointCount` | `Int` | 

<br />

`ranges`

Parameter | Type | Description
--------- | ------- | -----------
`min` | `Int` | 
`max` | `Int` | 
`stepSmall` | `Int` |
`stepLarge` | `Int` | 
`step` | `Int` | 
`def` | `Int` | 


### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Plugin : Set parameter value



### HTTP & WS Request

`PUT http://InfiniTweak/api/plugins/<pluginId>/parameters/<parameter>`


#### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 
`parameter` | <ul><li>`active` <li> `volume` <li> `<Int:parameterId>`</ul> 

#### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------modifier
`value` | `Float` | 

### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Show UI

<aside class="warning">UI blocks server thread</aside>


Show a plugin's UI

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>/UI`


#### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
`pluginId` | `Int` | 


### Result

None

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 

## Plugin : Stop VNC

Stop streaming a plugin's UI via VNC/WebSocket

### HTTP Request

`GET http://InfiniTweak/api/plugins/<pluginId>/stopVNC`


#### URL Parameters

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

#### Body Parameters


Parameter | Type | Description
--------- | ------- | -----------
`clientIdA` | `Int` | 
`portIdA` | `Int`
`clientIdB` | `Int`
`portIdB` | `Int`

### Result

#### WebSocket Callback

`PATCHBAY_CONNECTION_ADDED ` <br />

### Error

Error | Reason
--------- | ------- 
`UNKNOWN` | 


## Patchbay : Disconnect




Remove a connection between two devices/plugins

### HTTP Request

`DELETE http://InfiniTweak/api/patchbay/connections/<connectionId>`

#### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
`connectionId`| `Int` | 


### Results

#### WebSocket Callback

`PATCHBAY_CONNECTION_REMOVED`

### Errors

Error | Reason 
--------- | ------- 
`UNKNOWN_ERROR` |  | 






# WebSocket Callback

## Engine : Started

### Callback Message
```
ENGINE_INITIALIZED
```


#### Results

None

## Engine : Closed

### Callback Message
```
ENGINE_CLOSED
```


#### Results

None



## Plugin : Added


### Callback Message
```
PLUGIN_ADDED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`pluginId`| `Int` | 
`pluginName`| `Str` | Plugin Name


## Patchbay : Client Added

### Callback Message
```
PATCHBAY_CLIENT_ADDED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`clientId`| `Int` | 
`clientIcon`| `Int` | 
`clientName`| `Str` | Plugin Name
`pluginId`| `Int` | <ul><li> `-1` : Not a plugin, look at `clientId` <li> `<int>` : Plugin ID</ul>

## Plugin : Port Added

### Callback Message
```
PATCHBAY_PORT_ADDED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`portName`| `Str` | 
`portId`| `Int` : Port ID | 
`clientId`| `Int` | 
`portFlag`| `Int` | Compatibility 

<aside class="warning">Doesn't work</aside>


## Patchbay : Connection Added

### Callback Message
```
PATCHBAY_CONNECTION_ADDED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`connectionId`| `Str` | 
`clientOutId`| `Int` | 
`portOutId`| `Int` | 
`clientInId`| `Int` | 
`portInId`| `Int` | 

## Patchbay : Connection Removed

### Callback Message
```
PATCHBAY_CONNECTION_REMOVED
```

#### Results

Parameter | Type | Description
--------- | ------- | -----------
`conenctionId`| `Str` | 
`portOutId`| `Int` | 
`portInId`| `Int` | 




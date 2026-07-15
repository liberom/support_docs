### GET /tailnet/{tailnet}/settings

Source: https://api.tailscale.com/api/v2/api

Retrieves the configuration settings for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/settings

### Description
Retrieves the configuration settings for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/settings

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **settings** (object) - Tailnet settings.

### Response Example
{
  "settings": {
    "autoApprove": false,
    "sshEnabled": true
  }
}
```

--------------------------------

### GET /tailnet/{tailnet}/logging/configuration

Source: https://api.tailscale.com/api/v2/api

Fetches the logging configuration for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/logging/configuration

### Description
Fetches the logging configuration for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/logging/configuration

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **configuration** (object) - Logging settings.

### Response Example
{
  "configuration": {
    "enabled": true,
    "logLevel": "info"
  }
}
```

--------------------------------

### GET /tailnet/{tailnet}/keys

Source: https://api.tailscale.com/api/v2/api

Lists all authentication keys for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/keys

### Description
Lists all authentication keys for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/keys

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **keys** (array) - List of key objects.

### Response Example
{
  "keys": [
    {
      "id": "key-123",
      "capabilities": {},
      "expires": "2025-01-01T00:00:00Z"
    }
  ]
}
```

--------------------------------

### GET /tailnet/{tailnet}/posture/integrations

Source: https://api.tailscale.com/api/v2/api

Retrieves device posture integration configurations for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/posture/integrations

### Description
Retrieves device posture integration configurations for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/posture/integrations

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **integrations** (array) - List of posture integration objects.

### Response Example
{
  "integrations": [
    {
      "id": "int-001",
      "type": "exampleProvider",
      "config": {}
    }
  ]
}
```

--------------------------------

### GET /tailnet/{tailnet}/webhooks

Source: https://api.tailscale.com/api/v2/api

Lists all webhook endpoints configured for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/webhooks

### Description
Lists all webhook endpoints configured for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/webhooks

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None
### Response
#### Success Response (200)
- **webhooks** (array) - List of webhook endpoint objects.

### Response Example
{
  "webhooks": [
    {
      "id": "wh-123",
      "": "https://example.com/webhook",
      "events": ["device_up", "device_down"]
    }
  ]
}
```

--------------------------------

### GET /tailnet/{tailnet}/dns/nameservers

Source: https://api.tailscale.com/api/v2/api

Retrieves the DNS nameserver configuration for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/dns/nameservers

### Description
Retrieves the DNS nameserver configuration for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/dns/nameservers

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **nameservers** (array) - List of DNS nameserver IPs.

### Response Example
{
  "nameservers": ["8.8.8.8", "8.8.4.4"]
}
```

--------------------------------

### Get Device Posture Attributes with Shell Curl

Source: https://api.tailscale.com/api/v2/api

Retrieves posture attributes for a specified device via API GET request. Requires deviceId as path parameter; OAuth scope is devices:posture_attributes:read. Returns a JSON object with attributes and expiries.

```Shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/attributes' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### GET /tailnet/{tailnet}/users

Source: https://api.tailscale.com/api/v2/api

Lists all users in the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/users

### Description
Lists all users in the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/users

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_Nonen
### Request Example
None

### Response
#### Success Response (200)
- **users** (array) - List of user objects.

### Response Example
{
  "users": [    {
      "id": "user-abc",
      "email": "user@example.com",
      "role": "admin"
    }
  ]
}
```

--------------------------------

### GET /api/v2/tailnet/{tailnet}/devices

Source: https://api.tailscale.com/api/v2/api

Lists the devices in a tailnet. You can optionally control the fields returned and filter the results.

```APIDOC
## GET /api/v2/tailnet/{tailnet}/devices

### Description
Lists the devices in a tailnet. You can optionally control the fields returned and filter the results.

### Method
GET

### Endpoint
/api/v2/tailnet/{tailnet}/devices

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The tailnet ID. Use `-` to reference the default tailnet of the access token.

#### Query Parameters
- **fields** (stringenum) - Optional - Controls whether the response returns **all** fields or only a predefined subset. Options: `all`, `default`.
- **`<field>=<value>`** (string) - Optional - Server-side filtering of devices. Fields must be top-level device properties (e.g., `isEphemeral`, `tags`). Multiple filters perform a logical AND.

### Request Example
```shell
curl 'https://api.tailscale.com/api/v2/tailnet/{tailnet}/devices' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

### Response
#### Success Response (200)
- **devices** (array) - A list of device objects.
  - **addresses** (array[string]) - The IP addresses assigned to the device.
  - **id** (string) - The unique identifier for the device.
  - **nodeId** (string) - The node ID of the device.
  - **user** (string) - The user associated with the device.
  - **name** (string) - The name of the device.
  - **hostname** (string) - The hostname of the device.
  - **clientVersion** (string) - The client version running on the device.
  - **updateAvailable** (boolean) - Indicates if an update is available for the client.
  - **os** (string) - The operating system of the device.
  - **created** (string) - The creation timestamp of the device.
  - **connectedToControl** (boolean) - Indicates if the device is connected to the control server.
  - **lastSeen** (string) - The last seen timestamp of the device.
  - **keyExpiryDisabled** (boolean) - Indicates if key expiry is disabled for the device.
  - **expires** (string) - The expiration timestamp for the device's key.
  - **authorized** (boolean) - Indicates if the device is authorized.
  - **isExternal** (boolean) - Indicates if the device is external.
  - **multipleConnections** (boolean) - Indicates if multiple connections are enabled.
  - **machineKey** (string) - The machine key of the device.
  - **nodeKey** (string) - The node key of the device.
  - **blocksIncomingConnections** (boolean) - Indicates if the device blocks incoming connections.
  - **enabledRoutes** (array[string]) - The routes enabled on the device.
  - **advertisedRoutes** (array[string]) - The routes advertised by the device.
  - **clientConnectivity** (object) - Information about the device's client connectivity.
  - **tags** (array[string]) - The tags associated with the device.
  - **tailnetLockError** (string) - Any error related to Tailscale Lock.
  - **tailnetLockKey** (string) - The Tailscale Lock key.
  - **sshEnabled** (boolean) - Indicates if SSH is enabled for the device.
  - **postureIdentity** (object) - Posture identity information for the device.
  - **isEphemeral** (boolean) - Indicates if the device is ephemeral.

#### Response Example
```json
{
  "devices": [
    {
      "addresses": [
        "100.87.74.78",
        "fd7a:115c:a1e0:ac82:4843:ca90:697d:c36e"
      ],
      "id": "92960230385",
      "nodeId": "n292kg92CNTRL",
      "user": "amelie@example.com",
      "name": "pangolin.tailfe8c.ts.net",
      "hostname": "pangolin",
      "clientVersion": "v1.36.0",
      "updateAvailable": false,
      "os": "linux",
      "created": "2022-12-01T05:23:30Z",
      "connectedToControl": true,
      "lastSeen": "2022-12-01T05:23:30Z",
      "keyExpiryDisabled": false,
      "expires": "2023-05-30T04:44:05Z",
      "authorized": false,
      "isExternal": false,
      "multipleConnections": true,
      "machineKey": "",
      "nodeKey": "nodekey:01234567890abcdef",
      "blocksIncomingConnections": false,
      "enabledRoutes": [
        "10.0.0.0/16",
        "192.168.1.0/24"
      ],
      "advertisedRoutes": [
        "10.0.0.0/16",
        "192.168.1.0/24"
      ],
      "clientConnectivity": {
        "endpoints": [
          "199.9.14.201:59128",
          "192.68.0.21:59128"
        ],
        "latency": {
          "Dallas": {
            "latencyMs": 60.463043
          },
          "New York City": {
            "preferred": true,
            "latencyMs": 31.323811
          }
        },
        "mappingVariesByDestIP": false,
        "clientSupports": {
          "hairPinning": false,
          "ipv6": false,
          "pcp": false,
          "pmp": false,
          "udp": false,
          "upnp": false
        }
      },
      "tags": [
        "tag:golink"
      ],
      "tailnetLockError": "",
      "tailnetLockKey": "",
      "sshEnabled": false,
      "postureIdentity": {
        "serialNumbers": [
          "CP74LFQJXM"
        ]
      },
      "isEphemeral": false
    }
  ]
}
```

#### Error Responses
- **404** - Tailnet not found.
- **500** - Internal server error.
- **504** - Request took too long to process, please try again later.
```

--------------------------------

### GET /api/v2/device/{deviceId}/routes

Source: https://api.tailscale.com/api/v2/api

Retrieves the list of subnet routes that a device is advertising and those that are enabled for it. Routes must be both advertised and enabled for a device to act as a subnet router or exit node.

```APIDOC
## GET /api/v2/device/{deviceId}/routes

### Description
Retrieve the list of subnet routes that a device is advertising, as well as those that are enabled for it. Routes must be both advertised and enabled for a device to act as a subnet router or exit node.

### Method
GET

### Endpoint
/api/v2/device/{deviceId}/routes

#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
None

### Request Example
```
curl -H "Authorization: Bearer YOUR_SECRET_TOKEN" \
     'https://api.tailscale.com/api/v2/device/{deviceId}/routes'
```

### Response
#### Success Response (200)
- **advertisedRoutes** (array string) - A list of subnet routes advertised by the device.
- **enabledRoutes** (array string) - A list of subnet routes enabled for the device.

#### Response Example
```json
{
  "advertisedRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ],
  "enabledRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ]
}
```

#### Error Responses
- **404**: Device not found.
- **500**: Internal server error.
- **504**: Gateway timeout.
```

--------------------------------

### GET /tailnet/{tailnet}/user-invites

Source: https://api.tailscale.com/api/v2/api

Retrieves pending user invites for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/user-invites

### Description
Retrieves pending user invites for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/user-invites

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **invites** (array) - List of invite objects.

### Response Example
{
  "invites": [
    {
 "id": "invite-789",
      "email": "newuser@example.com",
      "status": "pending"
    }
  ]
}
```

--------------------------------

### GET /tailnet/{tailnet}/contacts

Source: https://api.tailscale.com/api/v2/api

Fetches the contact preferences for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/contacts

### Description
Fetches the contact preferences for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/contacts

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **contacts** (object) - Contact preference settings.

### Response Example
{
  "contacts": {
    "email": "admin@example.com",
    "slack": "#alerts"
  }
}
```

--------------------------------

### GET /api/v2/device/{deviceId}

Source: https://api.tailscale.com/api/v2/api

Retrieves the details for a specified device in the tailnet. Supports optional query parameter to control the fields returned in the response. Requires OAuth scope 'devices:core:read'.

```APIDOC
## GET /api/v2/device/{deviceId}

### Description
Retrieve the details for the specified device. OAuth Scope: `devices:core:read`.

### Method
GET

### Endpoint
/api/v2/device/{deviceId}

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
- **fields** (string) - Optional - Optionally controls whether the response returns `all` fields or only a predefined subset. Options: `all` or `default`. If not supplied, defaults to `default`.

#### Request Body
None

### Request Example
```
curl 'https://api.tailscale.com/api/v2/device/{deviceId}' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

### Response
#### Success Response (200)
application/json - Successful operation.

#### Response Example
{
  "addresses": [
    "100.87.74.78",
    "fd7a:115c:a1e0:ac82:4843:ca90:697d:c36e"
  ],
  "id": "92960230385",
  "nodeId": "n292kg92CNTRL",
  "user": "amelie@example.com",
  "name": "pangolin.tailfe8c.ts.net",
  "hostname": "pangolin",
  "clientVersion": "v1.36.0",
  "updateAvailable": false,
  "os": "linux",
  "created": "2022-12-01T05:23:30Z",
  "connectedToControl": true,
  "lastSeen": "2022-12-01T05:23:30Z",
  "keyExpiryDisabled": false,
  "expires": "2023-05-30T04:44:05Z",
  "authorized": false,
  "isExternal": false,
  "multipleConnections": true,
  "machineKey": "",
  "nodeKey": "nodekey:01234567890abcdef",
  "blocksIncomingConnections": false,
  "enabledRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ],
  "advertisedRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ],
  "clientConnectivity": {
    "endpoints": [
      "199.9.14.201:59128",
      "192.68.0.21:59128"
    ],
    "latency": {
      "Dallas": {
        "latencyMs": 60.463043
      },
      "New York City": {
        "preferred": true,
        "latencyMs": 31.323811
      }
    },
    "mappingVariesByDestIP": false,
    "clientSupports": {
      "hairPinning": false,
      "ipv6": false,
      "pcp": false,
      "pmp": false,
      "udp": false,
      "upnp": false
    }
  },
  "tags": [
    "tag:golink"
  ],
  "tailnetLockError": "",
  "tailnetLockKey": "",
  "sshEnabled": false,
  "postureIdentity": {
    "serialNumbers": [
      "CP74LFQJXM"
    ]
  },
  "isEphemeral": false
}

#### Error Responses
- **400** (application/json) - Invalid ID supplied.
- **404** (application/json) - Device not found.
- **500** (application/json) - Internal server error.
- **504** (application/json) - Gateway timeout.
```

--------------------------------

### GET /device/{deviceId}/device-invites

Source: https://api.tailscale.com/api/v2/api

Lists device invites associated with a specific device.

```APIDOC
## GET /device/{deviceId}/device-invites

### Description
Lists device invites associated with a specific device.

### Method
GET

### Endpoint
/device/{deviceId}/device-inv

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - Identifier of the device.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **invites** (array) - List of device invite objects.

### Response Example
{
  "invites": [
    {
      "id": "dev-invite-456",
      "expires": "2025-06-01T00:00:00Z"
    }
  ]
}
```

--------------------------------

### Devices API Operations

Source: https://api.tailscale.com/api/v2/api

This section details the available operations for managing devices within your Tailscale tailnet. You can list devices, get individual device details, delete devices, and manage various device attributes like routes, authorization, names, tags, keys, and IP addresses.

```APIDOC
## Devices API Operations

### Description
Operations for managing devices within a Tailscale tailnet.

### Base URL
`https://api.tailscale.com/api/v2/`

### Authentication
API access token (tskey-api-xxxxx) via Basic Auth or Bearer Token.

### Endpoints

#### List Devices in Tailnet

##### Method
`GET`

##### Endpoint
`/tailnet/{tailnet}/devices`

##### Description
Retrieves a list of all devices within the specified tailnet.

##### Parameters

###### Path Parameters
* **tailnet** (string) - Required - The name of your tailnet.

###### Query Parameters
None

###### Request Body
None

#### Get Device Details

##### Method
`GET`

##### Endpoint
`/device/{deviceId}`

##### Description
Retrieves detailed information about a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
None

#### Delete Device

##### Method
`DELETE`

##### Endpoint
`/device/{deviceId}`

##### Description
Deletes a specific device from your tailnet.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device to delete.

###### Query Parameters
None

###### Request Body
None

#### Expire Device Key

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/expire`

##### Description
Expires the current key for a specific device, forcing it to reauthenticate.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
None

#### Get Device Routes

##### Method
`GET`

##### Endpoint
`/device/{deviceId}/routes`

##### Description
Retrieves the configured routes for a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
None

#### Set Device Routes

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/routes`

##### Description
Configures or updates the routes for a specific device. This typically involves providing a JSON body with route information.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
- **routes** (array) - Required - An array of route objects to be applied to the device.
  - **(object)**
    - **dest** (string) - Required - The destination CIDR for the route.
    - **via** (string) - Optional - The IP address of the exit node to use for this route.

### Request Example (Set Device Routes)
```json
{
  "routes": [
    {
      "dest": "100.64.0.0/10",
      "via": "100.101.102.103"
    }
  ]
}
```

#### Authorize Device

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/authorized`

##### Description
Authorizes a specific device, allowing it to connect to the tailnet.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
- **authorized** (boolean) - Required - Set to `true` to authorize the device.

### Request Example (Authorize Device)
```json
{
  "authorized": true
}
```

#### Rename Device

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/name`

##### Description
Renames a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
- **&lt;newName&gt;** (string) - Required - The new desired name for the device.

### Request Example (Rename Device)
```json
{
  "my-new-device-name": ""
}
```

#### Update Device Tags

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/tags`

##### Description
Updates the tags associated with a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
- **tags** (array) - Required - An array of tag strings to apply to the device. Tags should be prefixed with `tag:`.

### Request Example (Update Device Tags)
```json
{
  "tags": ["tag:dev", "tag:prod"]
}
```

#### Replace Device Key

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/key`

##### Description
Replaces the current key for a specific device. This forces the device to generate a new key and reauthenticate.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
None

#### Assign IP Address to Device

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/ip`

##### Description
Assigns a specific IP address from your tailnet range to a device. This is typically used for static IP configurations.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
- **ip** (string) - Required - The IP address to assign to the device (e.g., "100.101.102.103").

### Request Example (Assign IP Address)
```json
{
  "ip": "100.101.102.103"
}
```

#### Get Device Attributes

##### Method
`GET`

##### Endpoint
`/device/{deviceId}/attributes`

##### Description
Retrieves the custom attributes associated with a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.

###### Query Parameters
None

###### Request Body
None

#### Set Device Attribute

##### Method
`POST`

##### Endpoint
`/device/{deviceId}/attributes/{attributeKey}`

##### Description
Sets or updates a custom attribute for a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.
* **attributeKey** (string) - Required - The key of the attribute to set.

###### Query Parameters
None

###### Request Body
- **value** (string) - Required - The value to assign to the attribute.

### Request Example (Set Device Attribute)
```json
{
  "value": "my-attribute-value"
}
```

#### Delete Device Attribute

##### Method
`DELETE`

##### Endpoint
`/device/{deviceId}/attributes/{attributeKey}`

##### Description
Deletes a custom attribute from a specific device.

##### Parameters

###### Path Parameters
* **deviceId** (string) - Required - The unique identifier of the device.
* **attributeKey** (string) - Required - The key of the attribute to delete.

###### Query Parameters
None

###### Request Body
None

### Error Handling

Errors are returned with standard HTTP status codes. The response body may contain a JSON object with a `message` field providing more details:

```json
{
  "message": "additional error information"
}
```

### Pagination

The Tailscale API does not currently support pagination. All results are returned at once.
```

--------------------------------

### Set Custom Device Posture Attributes (Shell Curl)

Source: https://api.tailscale.com/api/v2/api

This example demonstrates how to set or update a custom posture attribute for a specific device using cURL. It includes the device ID and attribute key in the URL, and the attribute's value and an optional expiry time in the JSON request body. Ensure you replace 'YOUR_SECRET_TOKEN' with your actual authorization token.

```shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/attributes/{attributeKey}' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{
  "value": "my_value",
  "expiry": "2022-12-01T05:23:30Z"
}'
```

--------------------------------

### Get device details with Tailscale API

Source: https://api.tailscale.com/api/v2/api

Retrieves detailed information about a specific device using its ID or nodeId. Supports optional fields parameter to control response content. Requires devices:core:read OAuth scope.

```shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### Tailscale API Error Response in JSON

Source: https://api.tailscale.com/api/v2/api

This JSON example shows the structure of error responses from the Tailscale API. It is returned when an API request fails, providing a status code and a message field. No dependencies or inputs are needed; outputs vary by error. Limitations include lack of detailed error codes beyond HTTP status.

```json
{
  "message": "additional error information"
}
```

--------------------------------

### GET /tailnet/{tailnet}/acl

Source: https://api.tailscale.com/api/v2/api

Retrieves the ACL (Access Control List) policy file for the specified tailnet.

```APIDOC
## GET /tailnet/{tailnet}/acl

### Description
Retrieves the ACL (Access Control List) policy file for the specified tailnet.

### Method
GET

### Endpoint
/tailnet/{tailnet}/acl

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
_None_

### Request Example
None

### Response
#### Success Response (200)
- **acl** (object) - The ACL policy.

### Response Example
{
  "acl": {}
}
```

--------------------------------

### GET /api/v2/device/{deviceId}/attributes

Source: https://api.tailscale.com/api/v2/api

This endpoint retrieves all posture attributes for a specified device as a JSON object of key-value pairs. It requires the 'devices:posture_attributes:read' OAuth scope. The device ID can be the nodeId or numeric id.

```APIDOC
## GET /api/v2/device/{deviceId}/attributes

### Description
Retrieve all posture attributes for the specified device, including custom and node-related attributes with expiry information. OAuth Scope: `devices:posture_attributes:read`.

### Method
GET

### Endpoint
/api/v2/device/{deviceId}/attributes

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
None

### Request Example
No body required.

### Response
#### Success Response (200)
Returns a JSON object with `attributes` (key-value pairs of posture attributes) and `expiries` (expiry times for attributes).
- **attributes** (object) - Posture attributes, e.g., {"custom:myScore": 80, "node:os": "linux"}
- **expiries** (object) - Expiry dates for attributes, e.g., {"custom:myScore": "2024-04-23T18:25:43.511Z"}

#### Error Response (404)
Device not found.

#### Error Response (500)
Internal server error.

#### Error Response (504)
Gateway timeout.

#### Response Example (200)
{
  "attributes": {
    "custom:myScore": 80,
    "custom:diskEncryption": true,
    "custom:myAttribute": "my_value",
    "node:os": "linux",
    "node:osVersion": "5.19.0-42-generic",
    "node:tsReleaseTrack": "stable",
    "node:tsVersion": "1.40.0",
    "node:tsAutoUpdate": false,
    "node:tsStateEncrypted": false
  },
  "expiries": {
    "custom:myScore": "2024-04-23T18:25:43.511Z"
  }
}
```

--------------------------------

### Delete Custom Device Posture Attributes (Shell Curl)

Source: https://api.tailscale.com/api/v2/api

This example shows how to delete a custom posture attribute from a device using cURL. It requires the device ID and the attribute key in the URL, and an authorization token in the header. This operation is intended for user-managed attributes within the 'custom:' namespace.

```shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/attributes/{attributeKey}' \
  --request DELETE \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### List Tailnet Devices with cURL

Source: https://api.tailscale.com/api/v2/api

This snippet demonstrates how to list devices in a Tailscale tailnet using the cURL command-line tool. It requires an authentication token and specifies the tailnet to query. The response includes a list of devices with their associated details.

```shell
curl 'https://api.tailscale.com/api/v2/tailnet/{tailnet}/devices' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### Set device tags via Tailscale API

Source: https://api.tailscale.com/api/v2/api

Assigns tags to a device by posting a JSON array of tag strings. Requires OAuth scope `devices:core` and the device ID. Successful response is 200.

```Shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/tags' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{
  "tags": [
    "tag:foo",
    "tag:bar"
  ]
}'
```

--------------------------------

### POST /api/v2/device/{deviceId}/attributes/{attributeKey}

Source: https://api.tailscale.com/api/v2/api

This endpoint allows creating or updating a custom posture attribute on a specified device. The attribute key must be prefixed with 'custom:' and is available for Personal and Enterprise plans. It supports string, number, or boolean values with optional expiry and comment fields.

```APIDOC
## POST /api/v2/device/{deviceId}/attributes/{attributeKey}

### Description
Create or update a custom posture attribute on the specified device. User-managed attributes must be in the custom namespace, indicated by prefixing the attribute key with `custom:`. Custom device posture attributes are available for the Personal and Enterprise plans. OAuth Scope: `devices:posture_attributes`.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/attributes/{attributeKey}

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.
- **attributeKey** (string) - Required - The name of the posture attribute to set. This must be prefixed with `custom:`. Keys have a maximum length of 50 characters including the namespace, and can only contain letters, numbers, underscores, and colon. Keys are case-sensitive. Keys must be unique, but are checked for uniqueness in a case-insensitive manner.

#### Query Parameters
None

#### Request Body
- **value** (string, number, or boolean) - Required - A value can be either a string, number or boolean. A string value can have a maximum length of 50 characters, and can only contain letters, numbers, underscores, and periods. A number value is an integer and must be a JSON safe number (up to 2^53 - 1).
- **expiry** (string) - Optional - An optional expiry time for a given posture attribute in date-time format. If set, Tailscale will automatically remove the attribute within a few minutes after the specified time.
- **comment** (string) - Optional - An optional comment indicating a reason why an attribute is set, which will be added to the audit log. Maximum length: 200 characters.

### Request Example
```json
{
  "value": "my_value",
  "expiry": "2022-12-01T05:23:30Z"
}
```

### Response
#### Success Response (200)
- **attributes** (object) - Contains the posture attributes including the newly set custom attribute.
- **expiries** (object) - Contains expiry times for attributes if applicable.

#### Response Example
```json
{
  "attributes": {
    "custom:myScore": 80,
    "custom:diskEncryption": true,
    "custom:myAttribute": "my_value",
    "node:os": "linux",
    "node:osVersion": "5.19.0-42-generic",
    "node:tsReleaseTrack": "stable",
    "node:tsVersion": "1.40.0",
    "node:tsAutoUpdate": false,
    "node:tsStateEncrypted": false
  },
  "expiries": {
    "custom:myScore": "2024-04-23T18:25:43.511Z"
  }
}
```

#### Error Responses
- **404** - Device not found.
- **500** - Internal server error.
- **504** - Gateway timeout.
```

--------------------------------

### POST /api/v2/device/{deviceId}/routes

Source: https://api.tailscale.com/api/v2/api

Sets a device's enabled subnet routes by replacing the existing list of subnet routes with the supplied parameters. Advertised routes cannot be set through the API.

```APIDOC
## POST /api/v2/device/{deviceId}/routes

### Description
Set a device's enabled subnet routes by replacing the existing list of subnet routes with the supplied parameters. Advertised routes cannot be set through the API, since they must be set directly on the device.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/routes

#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **routes** (array string) - Required - The new list of enabled subnet routes.

### Request Example
```
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_SECRET_TOKEN" \
     -d '{
       "routes": [
         "10.0.0.0/16",
         "192.168.1.0/24"
       ]
     }' \
     'https://api.tailscale.com/api/v2/device/{deviceId}/routes'
```

### Response
#### Success Response (200)
- **advertisedRoutes** (array string) - A list of subnet routes advertised by the device.
- **enabledRoutes** (array string) - A list of subnet routes enabled for the device.

#### Response Example
```json
{
  "advertisedRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ],
  "enabledRoutes": [
    "10.0.0.0/16",
    "192.168.1.0/24"
  ]
}
```

#### Error Responses
- **404**: Device not found.
- **500**: Internal server error.
- **504**: Gateway timeout.
```

--------------------------------

### List Device Routes - Shell Curl

Source: https://api.tailscale.com/api/v2/api

Retrieves the list of subnet routes that a device is advertising and those that are enabled for it. Requires the device ID and an authorization token. Returns a JSON object with advertised and enabled routes.

```curl
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/routes' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### Authenticate Tailscale API with cURL

Source: https://api.tailscale.com/api/v2/api

This code demonstrates authentication for Tailscale API requests using cURL commands. It requires a valid API access token (tskey-api-xxxxx). The input is the token, and output is the API response. Limitations include token expiration and user permissions; alternatively, OAuth clients can be used for scoped access.

```shell
// passing token with basic auth
curl -u "tskey-api-xxxxx:" https://api.tailscale.com/api/v2/...

// passing token as bearer token
curl -H "Authorization: Bearer tskey-api-xxxxx" https://api.tailscale.com/api/v2/...
```

--------------------------------

### Set Device Routes - Shell Curl

Source: https://api.tailscale.com/api/v2/api

Sets a device's enabled subnet routes by replacing the existing list with the provided routes. Requires the device ID, an authorization token, and a JSON body containing the new list of routes. Returns a JSON object with the updated advertised and enabled routes.

```curl
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/routes' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{ \
  "routes": [ \
    "10.0.0.0/16", \
    "192.168.1.0/24" \
  ] \
}'
```

--------------------------------

### POST /api/v2/device/{deviceId}/name

Source: https://api.tailscale.com/api/v2/api

Sets the device name for a device in your tailnet. The device name is the canonical name for the device and is generated from its OS hostname upon addition. Changes propagate immediately, so any existing Magic DNS URLs using the old name will become invalid.

```APIDOC
## POST /api/v2/device/{deviceId}/name

### Description
Sets the device name for a device in your tailnet. The device name is the canonical name for the device and is generated from its OS hostname upon addition. Changes propagate immediately, so any existing Magic DNS URLs using the old name will become invalid.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/name

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **name** (string) - Required - The new name for the device. This can be provided as either the fully qualified domain name (e.g., "nodename.your-domain.ts.net") or just the base name (e.g., "nodename"). If `name` is unset or provided empty, the device's name is reset to be generated from its OS hostname.

### Request Example
```json
{
  "name": "dev-server"
}
```

### Response
#### Success Response (200)
Successful operation.

#### Response Example
(No body provided for success response)

#### Error Responses
- **404** - Device not found.
- **500** - Internal server error.
- **504** - Gateway timeout.
```

--------------------------------

### Set device name via Tailscale API

Source: https://api.tailscale.com/api/v2/api

Updates the device's name by sending a POST request with a JSON body containing the new name. Requires OAuth scope `devices:core` and the device ID in the URL. Returns 200 on success.

```Shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/name' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{
  "name": "dev-server"
}'
```

--------------------------------

### POST /api/v2/device/{deviceId}/key

Source: https://api.tailscale.com/api/v2/api

Updates the key expiry settings for a device. This allows disabling key expiry or re-enabling it with the original expiry time.

```APIDOC
## POST /api/v2/device/{deviceId}/key

### Description
Updates the key expiry settings for a device. This allows disabling key expiry or re-enabling it with the original expiry time.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/key

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **keyExpiryDisabled** (boolean) - Required - If `true`, disable the device's key expiry. The original key expiry time is still maintained. Upon re-enabling, the key will expire at that original time. If `false`, enable the device's key expiry. Sets the key to expire at the original expiry time prior to disabling. The key may already have expired. In that case, the device must be re-authenticated.

### Request Example
```json
{
  "keyExpiryDisabled": true
}
```

### Response
#### Success Response (200)
Successful operation.

#### Response Example
(No body provided for success response)

#### Error Responses
- **404** - Device not found.
- **500** - Internal server error.
- **504** - Gateway timeout.
```

--------------------------------

### Authorize Device - Shell Curl

Source: https://api.tailscale.com/api/v2/api

Authorizes or deauthorizes a device for tailnets where device authorization is required. Requires the device ID, an authorization token, and a JSON body indicating the authorization status (true for authorize, false for deauthorize). Returns a success message upon completion.

```curl
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/authorized' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data 'null'
```

--------------------------------

### POST /api/v2/device/{deviceId}/tags

Source: https://api.tailscale.com/api/v2/api

Assigns or updates the list of tags for a specific device. Tags provide an identity separate from human users and can be used in ACLs for access control. A single device can have multiple tags assigned.

```APIDOC
## POST /api/v2/device/{deviceId}/tags

### Description
Assigns or updates the list of tags for a specific device. Tags provide an identity separate from human users and can be used in ACLs for access control. A single device can have multiple tags assigned.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/tags

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **tags** (array of strings) - Required - The new list of tags for the device. Example: `["tag:foo", "tag:bar"]`

### Request Example
```json
{
  "tags": [
    "tag:foo",
    "tag:bar"
  ]
}
```

### Response
#### Success Response (200)
Successful operation.

#### Response Example
(No body provided for success response)

#### Error Responses
- **400** - Bad request.
- **500** - Internal server error.
- **504** - Gateway timeout.
```

--------------------------------

### POST /tailnet/{tailnet}/acl

Source: https://api.tailscale.com/api/v2/api

Updates the ACL policy file for the specified tailnet.

```APIDOC
## POST /tailnet/{tailnet}/acl

### Description
Updates the ACL (Access Control List) policy file for the specified tailnet.

### Method
POST

### Endpoint
/tailnet/{tailnet}/acl

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - The name of the tailnet.

### Query Parameters
_None_

### Request Body
- **acl** (object) - Required - The new ACL definition.

### Request Example
{
  "acl": {
    "Groups": {},
    "Hosts": {},
    "TagOwners": {},
    "ACLs": []
  }
}

### Response
#### Success Response (200)
- **message** (string) - Confirmation that the ACL was updated.

### Response Example
{
  "message": "ACL updated successfully"
}
```

--------------------------------

### POST /api/v2/device/{deviceId}/authorized

Source: https://api.tailscale.com/api/v2/api

Authorizes or deauthorizes a device for tailnets where device authorization is required. The authorization status is determined by the `authorized` field in the payload.

```APIDOC
## POST /api/v2/device/{deviceId}/authorized

### Description
This call marks a device as authorized or revokes its authorization for tailnets where device authorization is required, according to the authorized field in the payload.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/authorized

#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **authorized** (boolean) - Required - If `true`, authorize a new device or re-authorize a previously deauthorized device. If `false`, deauthorize an authorized device.

### Request Example
```
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_SECRET_TOKEN" \
     -d 'null' \
     'https://api.tailscale.com/api/v2/device/{deviceId}/authorized'
```

### Response
#### Success Response (200)
Successful operation.

#### Response Example
(No specific response body provided for success, likely an empty or minimal response indicating success.)

#### Error Responses
- **404**: Device not found.
- **500**: Internal server error.
- **504**: Gateway timeout.
```

--------------------------------

### Update device key expiry via Tailscale API

Source: https://api.tailscale.com/api/v2/api

Enables or disables a device's key expiry by posting a boolean `keyExpiryDisabled`. Requires OAuth scope `devices:core` and the device ID. Returns 200 on success.

```Shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/key' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{
  "keyExpiryDisabled": true
}'
```

--------------------------------

### Expire device key with Tailscale API

Source: https://api.tailscale.com/api/v2/api

Marks a device's node key as expired, forcing the device to re-authenticate. The device must belong to the requesting user's tailnet. Requires devices:core OAuth scope.

```shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/expire' \
  --request POST \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

--------------------------------

### Set Device IPv4 with Shell Curl

Source: https://api.tailscale.com/api/v2/api

Sets a specific IPv4 address for a Tailscale device via API POST request. Requires deviceId as path parameter and ipv4 in JSON body; OAuth scope is devices:core. Note that changing IP may disrupt connections and require reconnection.

```Shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/ip' \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN' \
  --data '{
  "ipv4": "100.80.0.1"
}'
```

--------------------------------

### POST /api/v2/device/{deviceId}/expire

Source: https://api.tailscale.com/api/v2/api

Marks a device's node key as expired, requiring re-authentication to reconnect to the tailnet. The device must belong to the requesting user's tailnet. Requires OAuth scope 'devices:core'.

```APIDOC
## POST /api/v2/device/{deviceId}/expire

### Description
Mark a device's node key as expired. This will require the device to re-authenticate in order to connect to the tailnet. The device must belong to the requesting user's tailnet. OAuth Scope: `devices:core`.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/expire

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
None

### Request Example
```
curl 'https://api.tailscale.com/api/v2/device/{deviceId}/expire' \
  --request POST \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

### Response
#### Success Response (200)
Successful operation. No body.

#### Error Responses
- **404** (application/json) - Device not found.
- **500** (application/json) - Internal server error.
- **504** (application/json) - Gateway timeout.
```

--------------------------------

### DELETE /api/v2/device/{deviceId}/attributes/{attributeKey}

Source: https://api.tailscale.com/api/v2/api

This endpoint allows deleting a custom posture attribute from a specified device. It only applies to user-managed attributes in the custom namespace prefixed with 'custom:'. It requires authentication with the appropriate OAuth scope.

```APIDOC
## DELETE /api/v2/device/{deviceId}/attributes/{attributeKey}

### Description
Delete a posture attribute from the specified device. This is only applicable to user-managed posture attributes in the custom namespace, indicated by prefixing the attribute key with `custom:`. OAuth Scope: `devices:posture_attributes`.

### Method
DELETE

### Endpoint
/api/v2/device/{deviceId}/attributes/{attributeKey}

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.
- **attributeKey** (string) - Required - The name of the posture attribute to delete. This must be prefixed with `custom:`. Keys have a maximum length of 50 characters including the namespace, and can only contain letters, numbers, underscores, and colon. Keys are case-sensitive.

#### Query Parameters
None

#### Request Body
None

### Request Example
No request body required.

### Response
#### Success Response (200)
Successful operation. No response body.

#### Error Responses
- **404** - Device not found.
- **500** - Internal server error.
- **504** - Gateway timeout.
```

--------------------------------

### POST /api/v2/device/{deviceId}/ip

Source: https://api.tailscale.com/api/v2/api

This endpoint sets a specific IPv4 address for a device in the tailnet, replacing the randomly assigned one. It requires the 'devices:core' OAuth scope and will disrupt existing connections, necessitating reconnection with the new IP. The device ID can be the nodeId or numeric id.

```APIDOC
## POST /api/v2/device/{deviceId}/ip

### Description
When a device is added to a tailnet, its Tailscale IPv4 address is set at random. This endpoint replaces the existing IPv4 address with a specific value, breaking any existing connections. Reconnect using the new IP and flush DNS cache if needed. OAuth Scope: `devices:core`.

### Method
POST

### Endpoint
/api/v2/device/{deviceId}/ip

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
- **ipv4** (string) - Required - The new IPv4 address for the device. Example: 100.80.0.1

### Request Example
{
  "ipv4": "100.80.0.1"
}

### Response
#### Success Response (200)
Successful operation. No body returned.

#### Error Response (404)
Device not found.

#### Error Response (500)
Internal server error.

#### Error Response (504)
Gateway timeout.

#### Response Example (200)
No Body
```

--------------------------------

### DELETE /api/v2/device/{deviceId}

Source: https://api.tailscale.com/api/v2/api

Deletes the specified device from its tailnet. The device must belong to the requesting user's tailnet; shared devices are not supported. Requires OAuth scope 'devices:core'.

```APIDOC
## DELETE /api/v2/device/{deviceId}

### Description
Deletes the device from its tailnet. The device must belong to the requesting user's tailnet. Deleting devices shared with the tailnet is not supported. OAuth Scope: `devices:core`.

### Method
DELETE

### Endpoint
/api/v2/device/{deviceId}

### Parameters
#### Path Parameters
- **deviceId** (string) - Required - ID of the device. Using the device's `nodeId` is preferred, but its numeric `id` value can also be used.

#### Query Parameters
None

#### Request Body
None

### Request Example
```
curl 'https://api.tailscale.com/api/v2/device/{deviceId}' \
  --request DELETE \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

### Response
#### Success Response (200)
Successful operation. No body.

#### Error Responses
- **400** (application/json) - Invalid device value.
- **500** (application/json) - Internal server error.
- **501** (application/json) - Device not owned by tailnet.
- **504** (application/json) - Gateway timeout.
```

--------------------------------

### Delete device from tailnet with Tailscale API

Source: https://api.tailscale.com/api/v2/api

Deletes a device from its tailnet. The device must belong to the requesting user's tailnet. Shared devices cannot be deleted. Requires devices:core OAuth scope.

```shell
curl 'https://api.tailscale.com/api/v2/device/{deviceId}' \
  --request DELETE \
  --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.
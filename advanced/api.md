---
order: 886
label: API
icon: beaker
---
## Описание 
![](/static/19.png)
Marzban предоставляет REST API, который позволяет разработчикам программно взаимодействовать со службами Marzban. Чтобы просмотреть документацию по API в Swagger UI или ReDoc, установите переменную в файле env:

```bash
nano /opt/marzban/.env
```

Изменяем в нем следующие переменные

```
`DOCS=True`
```
Перейдите в браузере  `http://YOUR_DOMAIN/docs` или `http://YOUR_DOMAIN/redoc`.


# MarzbanAPI
Unified GUI Censorship Resistant Solution Powered by Xray

## Version: 0.4.2

### /api/admin/token

#### POST
##### Summary:

Login For Access Token

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

### /api/admin

#### GET
##### Summary:

Get Current Admin

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### POST
##### Summary:

Create Admin

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 409 | Admin already exists |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/admin/{username}

#### PUT
##### Summary:

Modify Admin

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Admin not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### DELETE
##### Summary:

Remove Admin

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Admin not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/admins

#### GET
##### Summary:

Get Admins

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| offset | query |  | No | integer |
| limit | query |  | No | integer |
| username | query |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /sub/{token}/

#### GET
##### Summary:

User Subscription

##### Description:

Subscription link, V2ray and Clash supported

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| token | path |  | Yes | string |
| user-agent | header |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

### /sub/{token}/info

#### GET
##### Summary:

User Subscription Info

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| token | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

### /sub/{token}/{client_type}

#### GET
##### Summary:

User Subscription With Client Type

##### Description:

Subscription link, v2ray, clash, sing-box, outline and clash-meta supported

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| token | path |  | Yes | string |
| client_type | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 400 | Invalid subscription type |
| 422 | Validation Error |

### /api/system

#### GET
##### Summary:

Get System Stats

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/inbounds

#### GET
##### Summary:

Get Inbounds

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/hosts

#### GET
##### Summary:

Get Hosts

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### PUT
##### Summary:

Modify Hosts

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/core

#### GET
##### Summary:

Get Core Stats

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/core/restart

#### POST
##### Summary:

Restart Core

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/core/config

#### GET
##### Summary:

Get Core Config

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### PUT
##### Summary:

Modify Core Config

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user

#### POST
##### Summary:

Add User

##### Description:

Add a new user

- **username** must have 3 to 32 characters and is allowed to contain a-z, 0-9, and underscores in between
- **expire** must be an UTC timestamp
- **data_limit** must be in Bytes, e.g. 1073741824B = 1GB
- **proxies** dictionary of protocol:settings
- **inbounds** dictionary of protocol:inbound_tags, empty means all inbounds

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 409 | User already exists |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user/{username}

#### GET
##### Summary:

Get User

##### Description:

Get users information

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### PUT
##### Summary:

Modify User

##### Description:

Modify a user

- set **expire** to 0 to make the user unlimited in time, null to no change
- set **data_limit** to 0 to make the user unlimited in data, null to no change
- **proxies** dictionary of protocol:settings, empty means no change
- **inbounds** dictionary of protocol:inbound_tags, empty means no change

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### DELETE
##### Summary:

Remove User

##### Description:

Remove a user

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user/{username}/reset

#### POST
##### Summary:

Reset User Data Usage

##### Description:

Reset user data usage

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 409 | User already exists |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user/{username}/revoke_sub

#### POST
##### Summary:

Revoke User Subscription

##### Description:

Revoke users subscription (Subscription link and proxies)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/users

#### GET
##### Summary:

Get Users

##### Description:

Get all users

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| offset | query |  | No | integer |
| limit | query |  | No | integer |
| username | query |  | No | string |
| status | query |  | No | [UserStatus](#UserStatus) |
| sort | query |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/users/reset

#### POST
##### Summary:

Reset Users Data Usage

##### Description:

Reset all users data usage

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user/{username}/usage

#### GET
##### Summary:

Get User Usage

##### Description:

Get users usage

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |
| start | query |  | No | string |
| end | query |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user/{username}/set-owner

#### PUT
##### Summary:

Set Owner

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| username | path |  | Yes | string |
| admin_username | query |  | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/users/expired

#### DELETE
##### Summary:

Delete Expired

##### Description:

Delete expired users
- **passed_time** must be a timestamp
- This function will delete all expired users that meet the specified number of days passed and can't be undone.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| passed_time | query |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | No expired user found. |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user_template

#### GET
##### Summary:

Get User Templates

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| offset | query |  | No | integer |
| limit | query |  | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### POST
##### Summary:

Add User Template

##### Description:

Add a new user template

- **name** can be up to 64 characters
- **data_limit** must be in bytes and larger or equal to 0
- **expire_duration** must be in seconds and larger or equat to 0
- **inbounds** dictionary of protocol:inbound_tags, empty means all inbounds

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 409 | Template by this name already exists |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/user_template/{id}

#### GET
##### Summary:

Get User Template

##### Description:

Get User Template information with id

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 404 | User Template not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### PUT
##### Summary:

Modify User Template

##### Description:

Modify User Template

- **name** can be up to 64 characters
- **data_limit** must be in bytes and larger or equal to 0
- **expire_duration** must be in seconds and larger or equat to 0
- **inbounds** dictionary of protocol:inbound_tags, empty means all inbounds

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User Template not found |
| 409 | Template by this name already exists |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### DELETE
##### Summary:

Remove User Template

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | User Template not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/node/settings

#### GET
##### Summary:

Get Node

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Node not found |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/node

#### POST
##### Summary:

Add Node

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/node/{node_id}

#### GET
##### Summary:

Get Node

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| node_id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Node not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### PUT
##### Summary:

Modify Node

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| node_id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Node not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

#### DELETE
##### Summary:

Remove Node

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| node_id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Node not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/nodes

#### GET
##### Summary:

Get Nodes

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/node/{node_id}/reconnect

#### POST
##### Summary:

Reconnect Node

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| node_id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 403 | You're not allowed |
| 404 | Node not found |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /api/nodes/usage

#### GET
##### Summary:

Get Usage

##### Description:

Get nodes usage

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| start | query |  | No | string |
| end | query |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

##### Security

| Security Schema | Scopes |
| --- | --- |
| OAuth2PasswordBearer | |

### /

#### GET
##### Summary:

Base

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

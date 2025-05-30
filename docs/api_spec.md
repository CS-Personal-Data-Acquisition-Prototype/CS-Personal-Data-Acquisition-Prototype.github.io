# Data Acquisition API Specification

# 1. Revision History

Version | Date | Author | Change Description
--- | --- | --- | ---
1.0 | 05/30/2025 | Garrett McMuchael | Updated session sensor data endpoints and added after datetime endpoint. Converted to markdown.
0.3 | 01/26/2025 | Lisa Young | Changed password hash & added password section
0.2 | 01/24/2025 | Garrett McMichael | Added numbering & security/auth sections
0.1 | 01/19/2025 | Garrett McMichael | Initial DL API specification creation

# 2. General Information

<table>
    <tr>
        <th>Description</th>
        <td>Facilitates decoupled communication between the TCP server and either the UI or Database layer through mutual API abstraction</td>
    </tr>
    <tr>
        <th>Purpose</th>
        <td>
            - Establish secure communication on public channels<br>
            - Decouple request dependency between layers<br>
            - Promote layer modularity through API abstraction<br>
            - Ensure data integrity through authentication and authorization
        </td>
    </tr>
    <tr>
        <th>Use Cases</th>
        <td>API is used by the public to securely route and analyze real-time data as well as access historical data for further analysis.</td>
    </tr>
</table>
<table>
    <tr>
        <th>Operation</th>
        <th>Create</th>
        <th>Read</th>
        <th>Update</th>
        <th>Delete</th>
    </tr>
    <tr>
        <th>Method</th>
        <td>POST</td>
        <td>GET</td>
        <td>PATCH</td>
        <td>DELETE</td>
    </tr>
</table>

# 3. HTTP Parameters

## 3.1 Headers

Header | Description
--- | ---
session_id | 128 bit session key provided by server in a cookie
Content-Type | Always set to application/json

## 3.2 Status Codes

Status Code | Usage
--- | ---
200 OK | Request successfully completed
201 Created | New resource successfully created
204 No Content | Request successfully completed. No content in response body.
400 Bad Request | Request incorrectly formatted. Response body includes error information.
401 Unauthorized | Invalid user credentials
403 Forbidden* | User lacks access to requested resource*
404 Not Found | Requested resource not found

*For sensitive resources - such as system files, testing endpoints, admin panels, or any functionality that could expose one user's existence to another - return a 404 ("Not Found") rather than a 403 ("Forbidden"). This approach hides the resource's existence and reduces the risk of targeted attacks or information disclosure.

# 4. Query Parameters

## 4.1 Pagination

| Syntax |
| --- |
| <host>/<path>?page_size=10&page_start_index=0 |

Parameter | Description
--- | ---
page_size | Integer representing rows per page
page_start_index | Integer representing page starting index

## 4.2 Sorting

| Syntax |
| --- |
| <host>/<path>?sort=[{“column”:“col1”, “dir”:”ASC”},{“column”:“col2”, “dir”:”DESC”}, {...}] |

Parameter | Description
--- | ---
sort | High priority first ordered array
column | Respective database column to sort on
dir | Ascending (ASC) or descending (DESC) order

## 4.3 Fields

| Syntax |
| --- |
| <host>/<path>?fields=col1,col2,col3 |

Parameter | Description
--- | ---
fields | A csv string containing desired column names to be returned

## 4.4 Filtering

| Syntax |
| --- |
| <host>/<path>?filter_type=all&filter=[{“column”:”col1”,“op”:”=”,”value”:”val”}, {...}] |

Parameter | Description
--- | ---
filter_type | all or any. all must match all filter criteria, any must match one.
filter | Integer representing page starting index
column | Respective database column to sort on
op | =, !=, <>, >=, <=, >, <, IN, LIKE, NOT_IN, NOT_LIKE. Defaults to =
value | Value compared as filter

# 5. Security

## 5.1 Data Transfer

Transfer Security | Solution
--- | ---
Key Exchange | Diffie-Hellman
Authentication | Digital signatures
Integrity | HMAC
Data Transfer | AES-128-CBC

## 5.2 Data Encryption

Confidential Data | Encryption Algorithm
--- | ---
User password | Argon2id
User secrets without access | SHA-256
User secrets with access | AES-256-CBC

## 5.3 Session

| SessionID Cookie |
| --- |
| Set-Cookie: session_id=<id>;HttpOnly;SameSite=Strict;Max-Age=3600;Path=/;Domain=<host> |

This cookie configuration:
- Blocks JavaScript access.
- Protects against CSRF attacks.
- Expires after 1 hour.
- Limits the cookie’s scope to the / path and the host domain.
- Omits ‘Secure’ due to the implementation of custom encryption in place of HTTPS

## 5.4 Passwords

| Requirement |
| --- |
| Must be at least 10 characters long |
| Cannot be the same as the username |

# 6. Endpoints

## 6.1 Authentication

Endpoint | Description
--- | ---
POST /authentication/login | Attempts login with provided credentials
POST /authentication/logout | Logs out current user
POST /authentication/renew | Renews session tokens

## 6.2 User

Endpoint | Description
--- | ---
POST /users | Create a new user
GET /users | Get all users
GET /users/profile | Get user currently logged in
GET /users/{username} | Get a specific user by username
PATCH /users/{username} | Partially or fully update a user
DELETE /users/{username} | Delete a user by username

## 6.3 Sensor

Endpoint | Description
--- | ---
POST /sensors | Create a new sensor
GET /sensors | Get all sensors
GET /sensors/{id} | Get a specific sensor by id
PATCH /sensors/{id} | Partially or fully update a sensor
DELETE /sensors/{id} | Delete a sensor by id

## 6.4 Session

Endpoint | Description
--- | ---
POST /sessions | Create a new session
GET /sessions | Get all sessions
GET /sessions/user/{username} | Get all sessions by user
GET /sessions/id/{id} | Get a specific session by id
PATCH /sessions/{id} | Partially or fully update a session
DELETE /sessions/{id} | Delete a session by id

## 6.5 Session Sensor

Endpoint | Description
--- | ---
POST /sessions-sensors | Link a new sensor to a session
GET /sessions-sensors | Get all session sensor linkages
GET /sessions-sensors/session/{session_id} | Get all sensors linked to a specific session
GET /sessions-sensors/session-sensor/{id} | Get a specific session sensor linkage by id
PATCH /sessions-sensors/{id} | Partially or fully update a session sensor link
DELETE /sessions-sensors/{id} | Delete a session sensor linkage by id

## 6.6 Session Sensor Data

Endpoint | Description
---|---
POST /sessions-sensors-data | Create a new datapoint
POST /sessions-sensors-data/batch | Batch create new datapoints
GET /sessions-sensors-data | Get all datapoints
GET /sessions-sensors-data/session/{session_id} | Get all datapoints linked to a specific session
GET /sessions-sensors-data/session/{session_id}/{datetime} | View All Datapoints by SessionID after Datetime
GET /sessions-sensors-data/id/{id} | Get all datapoints by session sensor id
GET /sessions-sensors-data/{id}/{datetime} | Get a specific datapoint
PATCH /sessions-sensors-data/{id}/{datetime} | Partially or fully update a specific datapoint
DELETE /sessions-sensors-data/{id}/{datetime} | Delete a specific datapoint

# 7. Authentication

## 7.1 Login
POST /authentication/login

### Request

Type | Property | Description
---|---|---|
String | username | Username of user
String | password_hash | Hashed password of user

### Response
#### Successful - 201

Type | Property | Description
---|---|---|
Cookie | session_id | Id of session

#### Request failed - 401

Type | Property | Description
---|---|---|
String | error | Contains “Invalid authentication credentials”

## 7.2 Logout
POST /authentication/logout

### Request

Type | Property | Description
---|---|---|
Cookie | session_id | Id of session

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 7.3 Renew Session
POST /authentication/renew

### Request

Type | Property | Description
---|---|---|
Cookie | session_id | Id of session

### Response
#### Successful - 201

Type | Property | Description
---|---|---|
Cookie | session_id | Id of session

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

# 8 User
## 8.1 Create User
POST /users

### Request

Type | Property | Description
---|---|---|
String | username | Username of user
String | password_hash | Hashed password of user

### Response
#### Creation successful - 201

Type | Property | Description
---|---|---|
String | username | Username of user

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 8.2 View All Users
GET /users

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | users | An array containing user usernames
String | users[n] | Username of user

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request unauthorized - 403

Type | Property | Description
---|---|---|
String | error | Contains “User not authorized”

## 8.3 View User Profile
GET /users/profile

### Request

Type | Property | Description
---|---|---|
Cookie | session_id | 128 bit session key provided by server

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | username | Username of user

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “User not found”

## 8.4 View User by Username
GET /users/{username}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | username | Username of user

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “User not found”

## 8.5 Update User
PATCH /users/{username}

### Request

Type | Property | Description
---|---|---|
String | username | Username of user
String | password_hash | Hashed password of user

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “User not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 8.6 Delete User
DELETE /users/{username}

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “User not found”

# 9 Sensor

## 9.1 Create Sensor
POST /sensors

### Request

Type | Property | Description
---|---|---|
String | type | Type of sensor

### Response
#### Creation successful - 201

Type | Property | Description
---|---|---|
String | id | Id of sensor
String | type | Type of sensor

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 9.2 View All Sensors
GET /sensors

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | sensors | An array containing sensor id and types
String | sensors[ ]. id | Id of sensor
String | sensors[ ]. type | Type of sensor

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request unauthorized - 403

Type | Property | Description
---|---|---|
String | error | Contains “User not authorized”

## 9.3 View Sensor by ID
GET /sensors/{id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | id | Id of sensor
String | type | Type of sensor

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Sensor not found”

## 9.4 Update Sensor
PATCH /sensors/{id}

### Request

Type | Property | Description
---|---|---|
String | id | Id of sensor
String | type | Type of sensor

### Response
#### Successful - 204

Type | Property | 
Description
---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Sensor not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 9.5 Delete Sensor
DELETE /sensor/{id}

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Sensor not found”

# 10 Session
## 10.1 Create Session
POST /sessions

### Request

Type | Property | Description
---|---|---|
String | username | Username of user

### Response
#### Creation successful - 201

Type | Property | Description
---|---|---|
String | id | Id of session
String | username | Username of user

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 10.2 View All Sessions
GET /sessions

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | sessions | Array containing session id and linked user
String | sessions[ ]. id | Id of session
String | sessions[ ]. username | Username of user

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

### Request unauthorized - 403

Type | Property | Description
---|---|---|
String | error | Contains “User not authorized”

## 10.3 View All Sessions by User
GET /sessions/user/{username}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | sessions | Array containing session id and linked user
String | sessions[ ]. id | Id of session
String | sessions[ ]. username | Username of user

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “User not found”

## 10.4 View Session by ID
GET /sessions/id/{id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | id | Id of session
String | username | Username of user

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

## 10.5 Update Session
PATCH /sessions/{id}

### Request

Type | Property | Description
---|---|---|
String | id | Id of session
String | username | Username of user

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 10.6 Delete Session
DELETE /sessions/{id}

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

# 11 Session Sensor
## 11.1 Create Session Sensor
POST /sessions-sensors

### Request

Type | Property | Description
---|---|---|
String | session_id | Id of session
String | sensor_id | Id of sensor

### Response
#### Creation successful - 201

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | session_id | Id of session
String | sensor_id | Id of sensor

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 11.2 View All Sessions Sensors
GET /sessions-sensors

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | sessions_sensors | Array containing session id and linked sensor
String | sessions_sensors[ ]. id | Id of session sensor
String | sessions_sensors[ ]. session_id | Id of session
String | sessions_sensors[ ]. sensor_id | Id of sensor

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request unauthorized - 403

Type | Property | Description
---|---|---|
String | error | Contains “User not authorized”

## 11.3 View All Sensors by SessionID
GET /sessions-sensors/session/{session_id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | sessions_sensors | Array containing session id and linked sensor
String | sessions_sensors[ ]. id | Id of session sensor
String | sessions_sensors[ ]. session_id | Id of session
String | sessions_sensors[ ]. sensor_id | Id of sensor

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

## 11.4 View Session Sensor by ID
GET /sessions-sensors/session-sensor/{id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | session_id | Id of session
String | sensor_id | Id of sensor

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

## 11.5 Update Session Sensor
PATCH /sessions-sensors/{id}

### Request

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | session_id | Id of session
String | sensor_id | Id of sensor

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 11.6 Delete Session Sensor
DELETE /sessions-sensors/{id}

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

# 12 Session Sensor Data
## 12.1 Create Datapoint
POST /sessions-sensors-data

### Request

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | datetime | Time of datapoint recording
JSON | data_blob | JSON string containing formatted sensor data

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 12.2 Batch Create Datapoint
POST /sessions-sensors-data/batch

### Request

Type | Property | Description
---|---|---|
Array | datapoints | Array holding session sensor data objects
String | datapoints[ ]. id | Id of session sensor
String | datapoints[ ]. datetime | Time of datapoint recording
JSON | datapoints[ ]. data_blob | JSON string containing formatted sensor data

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 12.3 View All Datapoints
GET /sessions-sensors-data

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | datapoints | Array holding session sensor data objects
String | datapoints[ ]. id | Id of session sensor data
String | datapoints[ ]. datetime | Time of datapoint recording
JSON | datapoints[ ]. data_blob | JSON string containing formatted sensor data

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request unauthorized - 403

Type | Property | Description
---|---|---|
String | error | Contains “User not authorized”

## 12.4 View All Datapoints by SessionID
GET /sessions-sensors-data/session/{session_id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | datapoints | Array holding session sensor data objects
String | datapoints[ ]. id | Id of session sensor data
String | datapoints[ ]. datetime | Time of datapoint recording
JSON | datapoints[ ]. data_blob | JSON string containing formatted sensor data

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session not found”

## 12.4 View All Datapoints by SessionID after Datetime
GET /sessions-sensors-data/session/{session_id}/{datetime}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | datapoints | Array holding session sensor data objects
String | datapoints[ ]. id | Id of session sensor data
String | datapoints[ ]. datetime | Time of datapoint recording
JSON | datapoints[ ]. data_blob | JSON string containing formatted sensor data

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “{request path} not found”

## 12.5 View All Datapoints by Session Sensor ID
GET /sessions-sensors-data/id/{id}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
Array | datapoints | Array holding session sensor data objects
String | datapoints[ ]. id | Id of session sensor data
String | datapoints[ ]. datetime | Time of datapoint recording
JSON | datapoints[ ]. data_blob | JSON string containing formatted sensor data

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

## 12.6 View Datapoints by ID and Datetime
GET /sessions-sensors-data/{id}/{datetime}

### Response
#### Successful - 200

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | datetime | Time of datapoint recording
JSON | data_blob | JSON string containing formatted sensor data

#### Request failed - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

## 12.7 Update Datapoint
PATCH /sessions-sensors-data/{id}/{datetime}

### Request

Type | Property | Description
---|---|---|
String | id | Id of session sensor
String | datetime | Time of datapoint recording
JSON | data_blob | JSON string containing formatted sensor data

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”

#### Request failed - 400

Type | Property | Description
---|---|---|
String | error | Description of request failure

## 12.8 Delete Datapoint
DELETE /sessions-sensors-data/{id}/{datetime}

### Response
#### Successful - 204

Type | Property | Description
---|---|---|
N/A | N/A | N/A

#### Unauthorized - 404*
*No information is revealed by avoiding 403 unauthorized

Type | Property | Description
---|---|---|
String | error | Contains “Session Sensor not found”
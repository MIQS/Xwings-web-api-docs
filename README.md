# Bitcoin Exchange Solution Web API
The Secure Web APIs are designed to allow client applications to view and update data using the HTTPS(rest) and WSS(websocket)
protocol over the internet. The purpose of this document is to provide the urls and the specification of the messages
communicated through Web APIs.

* [API Files](#apiFiles)
* [API General Info](#apiGeneralInfo)
* [Rest API General Info](#restApi)
* [Websocket API General Info](#websocketApi)

<a name="apiFiles" id="apiFiles"> </a>

## API Files
Following API files provide the details of the APIs that are available through different access channels.

File Name                             | Description
------------------------------------- | ---------------------------------------
rest-public-endpoints.md              | Details on rest public APIs
rest-authenticated-endpoints.md       | Details on rest authenticated APIs
websocket-public-endpoints.md         | Details on websocket public APIs
websocket-authenticated-endpoints.md  | Details on websocket authenticated APIs
errors.md                             | Details on API error codes

<a name="apiGeneralInfo" id="apiGeneralInfo"> </a>

## API General Info

### Message Format
All messages are in json format.

### Message Field Types

Type         | Description
------------ | ------------
Timestamp    | all timestamps from API are returned in ISO 8601 with microseconds e.g 2018-03-01T10:00:00.123456Z
Integer      | Integer numbers
Boolean      | True/False
DoubleString | Decimal numbers are returned as strings to preserve full precision across platforms
String       | Text

### Mandatory Field Indicators

Indicator    | Description
------------ | ------------
M            | Mandatory field
(M)          | Mandatory field under certain conditions
 O           | Optional field

<a name="restApi" id="restApi"> </a>

## REST API General Info

All requests and responses use application/json content type. Responses	follow HTTP response status codes to indicate
the success and the failure.

### Success/Error Response

Successful http response contains HTTP status code 200 and an optional body. If the response contains the body,
the fields within the body are documented in each related API sections.  Failed http response contains non 200 HTTP status
code and the body with an errorCode field to indicate the cause of the failures.

#### Error Response Fields

Name         | Type        | Description
------------ | ------------| ----------------
errorCode    | String      | Error code. e.g.INVALID_PASSWORD

### Pagination

Pagination is supported for all REST calls that return arrays. The newest items are returned by default.

Name	   |Type(value)|Mandatory|Description
-----------| ----------|---------|-------------------
pageNumber | Integer   | O       | Default to 1
pageSize   | Integer   | O	     | Default to 100

Example: GET api/orders?pageNumber=1&pageSize=100

### Rate Limits

* Throttle public endpoints by IP: 5 requests per second
* Throttle authenticated endpoints by user ID: 5 requests per second

<a name="websocketApi" id="websocketApi"> </a>

## WEBSOCKET API General Info

wss://ws-api.xxxx.com

All messages sent and received through websocket are encoded in JSON
format. All messages have a **type** attribute that can be used to
handle the message.

Failures will cause an error message to be emitted with **errorCode**.

#### Error Response Fields
Name          | Type(value) | Mandatory |Description
--------------|-------------|-----------|---------------------------
type          | error       | M         | Error message type
userMessageId |	Integer	    |(M)	    | Mandatory if userMessageId is provided in the user request
errorCode	  | String      | M	        | Error code


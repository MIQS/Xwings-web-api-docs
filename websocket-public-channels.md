# Websocket Public Channels
* [Ticker](#ticker)
* [Order Book](#orderBook)
* [Full Order Book channel](#fullOrderBook)
* [Trade](#trade)
* [Charts](#charts)

<a name="ticker" id="ticker"> </a>
---
## Ticker

ticker data is pushed every second.

### Request Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel        | ticker                          | M           | 
userMessageId  | Integer                         | O           | Unique message id for this websocket session
instrumentIds  | Array of instrumentId Strings   | M           | 


### Response Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribed/unsubscribed         | M           | Subscribed/Unsubscribed message type
channel        | ticker                          | M           | 
timestamp      | Timestamp                       | M           | Request accepted time
instrumentIds  | Array of instrumentId Strings   | M           | 
userMessageId  | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields:

Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | ticker         | M           | 
timestamp      | Timestamp      | M           | Ticker created time
instrumentId   | String         | M           | e.g. “BTCUSD”
lastPrice      | DoubleString   | M           | 
bestBid        | DoubleString   | M           | 
bestAsk        | DoubleString   | M           | 
24hHigh        | DoubleString   | M           | 
24hLow         | DoubleString   | M           | 
24hVolume      | DoubleString   | M           | 
24hChange      | DoubleString   | M           | 



<a name="orderBook" id="orderBook"> </a>
---
## Order Book

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           | 
depth          | Integer                        | O           | Default to 25
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribed/unsubscribed        | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           | 
timestamp      | Timestamp                      | M           | When subscription request was accepted
depth          | Integer                        | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name           | Type(value)                        |  Mandatory  | Description
---------------| -----------------------------------| ------------|--------------------------------------
type           | orderBook                          | M           |
timestamp      | Timestamp                          | M           | order book update time
instrumentId   | String                             | M           |
bids           | Array of [price, size, numOfOrders]| M           | The aggregated size for each price level is returned with numOfOrders count for the price
asks           | Array of [price, size, numOfOrders]| M           | The aggregated size for each price level is returned with numOfOrders count for the price


The initial bids and asks contain the full depth that the user
subscribes for. The subsequent messages only contain the updates.

<a name="fullOrderBook" id="fullOrderBook"> </a>

---
## Full Order Book channel

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                  | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribed/unsubscribed        | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                  | M           | 
timestamp      | Timestamp                      | M           | When the subscription was accepted
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields

Name           | Type(value)     | Mandatory   | Description
---------------| ----------------|-------------|-------------
type           | fullOrderBook   | M           | 
timestamp      | Timestamp       | M           | order book update time
instrumentId   | String          | M           | 
orderId        | String          | M           | 
price          | DoubleString    | M           | 
remainingSize  | DoubleString    | M           | 
side           | Enum            | M           |
sequence       | LongString      | M           | 

The initial bids and asks contain the full depth that the user
subscribes for. The subsequent messages only contain the updates.

<a name="trade" id="trade"> </a>

---
## Trade

trade data is pushed whenever a trade occurs in the system.  

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribed/unsubscribe         | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           | 
timestamp      | Timestamp                      | M           | When the subscription request was accepted
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-------------
type             | trade           | M           | 
timestamp        | Timestamp       | M           | Trade time
instrumentId     | String          | M           | 
time      | Timestamp       | M           | 
tradeId   | String          | M           | 
price     | DoubleString    | M           | 
size      | DoubleString    | M           | 
side      | Enum            | M           | Buy/Sell



<a name="charts" id="charts"> </a>

---
## Charts

### Request Fields

Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           | 
instrumentIds   | Array of instrumentId Strings  | M           | 
userMessageId   | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribed/unsubscribe         | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           | 
timestamp       | Timestamp                      | M           | When the subscription request was accepted
instrumentIds   | Array of instrumentId Strings  | M           | 
userMessageId   | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name          | Type(value)   | Mandatory   | Description
--------------| --------------|-------------|-------------
type          | charts        | M           | 
timestamp     | Timestamp     | M           | Chart update time
instrumentId  | String        | M           | 
startTime     | Timestamp     | M           | 
openPrice     | String        | M           | 
closePrice    | String        | M           | 
low           | String        | M           | 
high          | String        | M           | 
volume        | String        | M           | 


The first charts message will contain the array of historical data
entries with the size of 60.


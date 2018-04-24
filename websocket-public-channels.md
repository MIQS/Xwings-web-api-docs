# Websocket Public Channels
* [Ticker](#ticker-1)
* [Order Book](#order-book-1)
* [Full Order Book channel](#full-order-book-channel)
* [Trade](#trade-1)
* [Charts](#charts-1)

<a name="ticker-1" id="ticker-1"> </a>

## Ticker

### Request Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribe/unsubscribe                       | M           | Subscribe/Unsubscribe message type
channel        | ticker                          | M           | 
userMessageId  | Integer                         | O           | Unique message id for this websocket session
instrumentIds  | Array of instrumentId Strings   | M           | 


### Response Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribed/unsubscribed                       | M           | Subscribed/Unsubscribed message type
channel        | ticker                          | M           | 
instrumentIds  | Array of instrumentId Strings   | M           | 
userMessageId  | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields:

Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | ticker         | M           | 
instrumentId   | String         | M           | e.g. “BTCUSD”
time           | Timestamp      | M           | 
lastPrice      | DoubleString   | M           | 
bestBid        | DoubleString   | M           | 
bestAsk        | DoubleString   | M           | 
24hHigh        | DoubleString   | M           | 
24hLow         | DoubleString   | M           | 
24hVolume      | DoubleString     | M           | 
24hChange      | DoubleString   | M           | 



<a name="order-book-1" id="order-book-1"> </a>

## Order Book

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           | 
depth          | Integer                        | O           | Default to 25
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribed/unsubscribed                      | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           | 
depth          | Integer                        | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name           | Type(value)                            | Description
---------------| ---------------------------------------|--------------------------------------
type           | orderBook                              |  
instrumentId   | String                                 | 
time           | Timestamp                              | 
bids           | Array of [price, size, numOfOrders]    | The aggregated size for each price level is returned with numOfOrders count for the price
asks           | Array of [price, size, numOfOrders]    | The aggregated size for each price level is returned with numOfOrders count for the price


The initial bids and asks contain the full depth that the user
subscribes for. The subsequent messages only contain the updates.



<a name="full-order-book-channel" id="full-order-book-channel"> </a>


## Full Order Book channel

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                  | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribed/unsubscribed                      | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                  | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name           | Type(value)     | Mandatory   | Description
---------------| ----------------|-------------|-------------
type           | fullOrderBook   | M           | 
instrumentId   | String          | M           | 
orderId        | String          | M           | 
price          | DoubleString    | M           | 
remainingSize  | DoubleString    | M           | 
status         | String          | M           | 
side           | String          | M           | 
sequence       | LongString      | M           | 


Sequence to process full order book:

1.  Subscribe for fullOrderBook channel

2.  Call REST to get order book snapshot

3.  Playback queued messages and ignore the ones with the smaller
    sequence in the messages.

4.  Apply the update to orderbook



<a name="trade-1" id="trade-1"> </a>


## Trade

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribe/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel        | trade                         | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribed/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name      | Type(value)     | Mandatory   | Description
----------| ----------------|-------------|-------------
type      | trade          | M           | 
instrumentId      | String          | M           | 
time      | Timestamp       | M           | 
tradeId   | String          | M           | 
price     | DoubleString    | M           | 
size      | DoubleString    | M           | 
side      | String          | M           | Buy/Sell



<a name="charts-1" id="charts-1"> </a>


## Charts

### Request Fields

Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribe/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           | 
instrumentIds   | Array of instrumentId Strings  | M           | 
userMessageId   | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribed/unsubscribe                      | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           | 
instrumentIds   | Array of instrumentId Strings  | M           | 
userMessageId   | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name          | Type(value)   | Mandatory   | Description
--------------| --------------|-------------|-------------
type          | charts        | M           | 
instrumentId      | String          | M           | 
startTime     | Timestamp     | M           | 
openPrice     | String        | M           | 
closePrice    | String        | M           | 
low           | String        | M           | 
high          | String        | M           | 
volume        | String        | M           | 


The first charts message will contain the array of historical data
entries with the size of 60.

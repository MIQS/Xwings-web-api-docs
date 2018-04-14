# REST Public Endpoints

* [Instruments](#instruments)
* [Ticker](#ticker)
* [Order Book](#order-book)
* [Trades](#trades)
* [Charts](#charts)

<a name="instruments" id="instruments"> </a>


## Instruments

GET /api/public/instruments

### Request Parameters

Name                  | Type(value)      | Mandatory   | Description
----------------------| -----------------|-------------|-----------------------
instrumentId          | String           | O           | 
productType           | String           | O           | Spot/Futures/Indexes
symbol                | String           | O           | 
quoteCurrency         | String           | O           | 
underlying            | String           | O           | 

### Success Response Body Fields

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. BTCUSD
symbol             | String           | M           | e.g. BTC
quoteCurrency      | String           | M           | e.g. USD
productType        | String           | M           | Spot/Futures/Indexes
tickSize           | DoubleString     | M           | e.g. 0.01
lotSize            | Integer          | (M)         | Mandatory for tradable Spot and Futures instruments e.g. 1
minOrderSize       | DoubleString     | (M)         | Mandatory for tradable Spot and Futures instruments
maxOrderSize       | DoubleString     | (M)         | Mandatory for tradable Spot and Futures instruments
expiry             | Timestamp        | (M)         | Mandatory for futures instrument
underlying         | String           | (M)         | Mandatory for futures instrument
contractMultipler  | Integer          | (M)         | Mandatory for futures instrument


### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------


## Ticker

GET /api/public/ticker

### Request Parameters

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. “BTCUSD”

### Success Response Body Fields

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | e.g. “BTCUSD”
time            | Timestamp        | M           | 
lastPrice       | DoubleString     | M           | 
bestBid         | DoubleString     | M           | 
bestAsk         | DoubleString     | M           | 
24hHigh         | DoubleString     | M           | 
24hLow          | DoubleString     | M           | 
24hVolume       | LongString       | M           | 
24hChange       | DoubleString     | M           | 

### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------

<a name="order-book" id="order-book"> </a>


## Order Book

GET /api/public/orderbook

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | e.g. “BTCUSD”
level           | Integer          | M           | 1 - top bid and ask;2 – order book;3 – full order level book

### Success Response Body Fields

Name            | Type(value)                                   | Mandatory   | Description
----------------| ----------------------------------------------|-------------|-----------------------
instrumentId    | String                                        | M           | 
level           | 1/2/3                                         | M           | 
sequence        | LongString                                    | M           | 
bids            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned
asks            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned


### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------

<a name="trades" id="trades"> </a>


## Trades

GET /api/public/trades

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 

### Success Response Body Fields

Name      | Type(value)      | Mandatory   | Description
----------| -----------------|-------------|-----------------------
time      | Timestamp        | M           | 
tradeId   | String           | M           | 
price     | DoubleString     | M           | 
size      | DoubleString     | M           | 
side      | String           | M           | Buy/Sell

### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------

<a name="charts" id="charts"> </a>


## Charts

GET /api/public/charts

It returns an array of data point stats.

### Request Parameters

Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
instrumentId  | String          | M           | 
startTime     | Timestamp       | M           | 
endTime       | Timestamp       | M           | 
granularity   | Integer         | M           | In seconds; 60/300/900/3600/21600/86400;The combination of startTime, endTime and granularity determines how many data points obtained. The maximum supported number of data points is xxx

### Success Response Body Fields

Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
startTime     | Timestamp       | M           | 
endTime       | Timestamp       | M           | 
openPrice     | String          | M           | 
closePrice    | String          | M           | 
low           | String          | M           | 
high          | String          | M           | 
volume        | String          | M           | 

### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------

<a name="private-endpoints" id="private-endpoints"> </a>


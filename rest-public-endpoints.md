# REST Public Endpoints

* [Instruments](#instruments)
* [Ticker](#ticker)
* [Order Book](#orderBook)
* [Trades](#trades)
* [Charts](#charts)
* [Time](#time)

<a name="instruments" id="instruments"> </a>

---
## Instruments

    GET /instruments

### Request Parameters

Name                  | Type(value)      | Mandatory   | Description
----------------------| -----------------|-------------|-----------------------------
instrumentId          | String           | O           | 
instrumentType        | Enum             | O           |
asset                 | String           | O           |
quoteAsset            | String           | O           |
underlying            | String           | O           | 

### Success Response Body Fields

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|--------------------------------
instrumentId       | String           | M           | e.g. BTCUSD
asset              | String           | M           | e.g. BTC
quoteAsset         | String           | M           | e.g. USD
instrumentType     | Enum             | M           | 
tickSize           | DoubleString     | M           | price increment
lotSize            | DoubleString     | M           | size increment
minOrderPrice      | DoubleString     | M           | 
maxOrderPrice      | DoubleString     | M           | 
minOrderSize       | DoubleString     | M           | 
maxOrderSize       | DoubleString     | M           | 
expiry             | Long             | (M)         | Mandatory for FUTURES instrument
underlying         | String           | (M)         | Mandatory for FUTURES instrument
contractMultiplier | Integer          | (M)         | Mandatory for FUTURES instrument

---
## Ticker

    GET /ticker

### Request Parameters

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. “ETHBTC”

### Success Response Body Fields

Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. “ETHBTC”
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
bestBid          | DoubleString     | M           | 
bestAsk          | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

---
<a name="orderBook" id="orderBook"> </a>

## Order Book

    GET /orderbook
    
    Weight: 5

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 
bookLevel       | Integer          | M           | 1 - top bid and ask; 2 – order book; 3 – full order level book

### Success Response Body Fields

Name               | Type(value)                                   | Mandatory   | Description
-------------------| ----------------------------------------------|-------------|-----------------------
instrumentId       | String                                        | M           |
lastModifiedTime   | Long                                          | M           | 
bookLevel       | Integer                                       | M           | 1/2/3
sequence        | Long                                          | M           | 
bids            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned
asks            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned

---
<a name="trades" id="trades"> </a>

## Trades

    GET /trades
    
Returns most recent trades in an array.

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 

### Success Response Body Array Json Fields

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
createdTime     | Long             | M           | 
tradeId   | String           | M           | 
price     | DoubleString     | M           | 
size      | DoubleString     | M           | 
side      | Enum             | M           |


<a name="charts" id="charts"> </a>

---
## Charts

    GET /charts

It returns an array of data point stats.

### Request Parameters

Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
instrumentId  | String          | M           | 
endTime       | Long            | M           | Seconds since Unix Epoch
granularity   | Integer         | M           | In seconds; 60/300/900/3600/21600/86400;The combination of startTime, endTime and granularity determines how many data points obtained. The maximum supported number of data points is xxx

### Success Response Body Fields

Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-----------------------
lastModifiedTime | Long            | M           |
startTime        | Long            | M           | 
endTime          | Long            | M           | 
openPrice        | String          | M           | 
closePrice       | String          | M           | 
low              | String          | M           | 
high             | String          | M           | 
volume           | String          | M           | 

<a name="time" id="time> </a>

---
## Time
   
    GET /time
   
It returns the server time in milliseconds since Unix Epoch

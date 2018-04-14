# REST Authenticated Endpoints

All requests authenticated APIs require authentication.  For each REST call, API_KEY, SIGNATURE and NONCE should be encoded in HTTP headers.

* [Orders](#orders)
* [OwnTrades](#owntrades)
* [New Order](#new-order)
* [Cancel Order](#cancel-order)
* [Cancel All Order](#cancel-all-order)
* [Accounts](#accounts)
* [Account Transactions](#account-transactions)
* [Withdraw](#withdraw)


<a name="orders" id="orders"> </a>

## Orders

GET /api/private/orders

	Returns an array of orders; Pagination is supported. Cancelled orders in
	the most recent 2 days are included, the older cancelled orders are not.

### Request Parameters

Name           | Type(value)                                 | Mandatory   | Description
---------------| --------------------------------------------|-------------|-------------------------------------------------------
orderId        | String                                      | O           | 
instrumentId   | String                                      | O           | If not provided, orders for all symbols are returned
status         | Open, Executed,Partial Executed, Cancelled  | O           | If not provided, orders for all status are returned

### Success Response Body Fields

Name                  | Type(value)                      | Mandatory   | Description
----------------------| ---------------------------------|-------------|-------------------------------------------------------------------------------
orderId               | String                           | M           | 
instrumentId          | String                           | M           | 
userAccount           | String                           | M           | User may have multiple accounts in firm user case.
type                  | Market, Limit, Stop, StopLimit   | M           | 
price                 | DoubleString                     | M           | 
size                  | DoubleString                     | M           | 
side                  | Buy/Sell                         | M           | 
timeInForce           | GTC, GTT, IOC, FOK               | M           | 
orderTime             | Timestamp                        | M           | 
stopPrice             | DoubleString                     | O           | 
status                | Open, Executed, Cancelled        | M           | 
executedSize          | DoubleString                     | O           | 
executedPrice         | DoubleString                     | O           | 
postLiquidity         | Boolean                          | M           | True – order rest in the book initially
fee                   | DoubleString                     | O           | 
selfTradePrevention   | String                           | M           | DC – Decrease and cancel,CO – Cancel oldest,CN – Cancel newestCB – Cancel both
clientOrderId         | String                           | O           | 

### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------


<a name="owntrades" id="owntrades"> </a>

---
## OwnTrades

GET /api/private/ownTrades

### Request Parameters

Name          | Type(value)  | Mandatory | Description          
--------------| -------------| ----------| ----------------------------------------------------
orderId       | String       | O         | 
instrumentId  | String       | O         | If not provided, orders for all symbols are returned

### Success Response Body Fields

Name          | Type(value)  | Mandatory | Description
--------------| -------------| ----------| ---------------------------------------
time          | Timestamp    | M         |
tradeId       | String       | M         |
userAccount   | String       | M         |
price         | DoubleString | M         |
size          | DoubleString | M         |
side          | String       | M         | Buy/Sell 
fee           | DoubleString | M         |
liquidity     | String       | M         | M – liquidity maker, T – liquidity taker


### Failure Error Codes

Error Code            | Description                  
----------------------| ---------------------------------


<a name="new-order" id="new-order"> </a>

---
## New Order

POST /api/private/newOrder

### Request Parameters:

Name                  | Type(value)        | Mandatory | Description
----------------------| -------------------| ----------| ----------------------------------------------------
instrumentId          | String             | M         | 
userAccount           | String             | M         | User account used for this order
orderType             | String             | M         | Limit/Market/Stop/StopLimit
price                 | DoubleString       | (M)       | Mandatory if order is non Market order
size                  | DoubleString       | (M)       | Mandatory if order is non Market order,For Market order, the user can either provide size or amount in quote currency
amount                | DoubleString       | O         | Amount in quote currency to buy/sell
side                  | Buy/Sell           | M         | 
timeInForce           | GTC, GTT, IOC, FOK | M         | 
clientOrderId         | String             | O         | 
stopPrice             | NumberString       | (M)       | Mandatory if orderType is Stop or StopLimit
postOnly              | Boolean            | O         | Default to false. If any part of the order results in taking liquidity, the order will be rejected and no part of it will execute.
selfTradePrevention   | String             | O         | Decrease and cancel (Default);Cancel oldest;Cancel newest;Cancel both;


### Success Response Body Fields

Name                  | Type(value)        | Mandatory | Description
----------------------| -------------------| ----------| ----------------------------------------------------
clientOrderId         | String             | (M)       | Mandatory if clientOrderId is provided by the user
orderId               | String             | M         | System generated unique order id


### Failure Error Codes

Error Code            | Description      
----------------------| -----------------


<a name="cancel-order" id="cancel-order"> </a>

---
## Cancel Order

POST /api/private/cancelOrder

### Request Parameters

Name               | Type(value)    | Mandatory | Description
-------------------| ---------------| ----------| -----------
orderId            | String         | M         | 
clientOrderId      | String         | (M)       | 


### Success Response Body Fields

Name               | Type(value)    | Mandatory | Description
-------------------| ---------------| ----------| -----------
orderId            | String         | (M)       | Mandatory if client order id is not provided
clientOrderId      | String         | (M)       | Mandatory if order id is not provided

### Failure Error Codes

Error Code            | Description      
----------------------| -----------------


<a name="cancel-all-order" id="cancel-all-order"> </a>

---
## Cancel All Order

POST /api/private/cancelAllOrders

### Success Response Body Fields

Name               | Type(value)       | Mandatory | Description
-------------------| ------------------| ----------| ----------------------------------------
orderIds           | Array of Strings  | M         | Orders that are cancelled in the system 


### Failure Error Codes

Error Code            | Description      
----------------------| -----------------

<a name="accounts" id="accounts"> </a>

---
## Accounts

GET /api/private/accounts

### Request Parameters

Name            | Type(value)   | Mandatory | Description
----------------| --------------| ----------| -------------------
userAccount     | String        | O         | Main account by default

### Success Response Body Fields

Name         | Type(value)   | Mandatory | Description
-------------| --------------| ----------| -------------------
accountId    | String        | M         | 
currency     | String        | M         | 
balance      | DoubleString  | M         |
available    | DoubleString  | M         | 

### Failure Error Codes

Error Code            | Description      
----------------------| -----------------


<a name="account-transactions" id="account-transactions"> </a>

---
## Account Transactions

GET /api/private/accountTransactions

	List all the account transactions that either increases or decreases the
	account balance and available balance. Pagination is supported.

### Request Parameters

Name            | Type(value)   | Mandatory | Description
----------------| --------------| ----------| -------------------
accountId       | String        | O         | 
transactionType | String        | O         | 
referenceId     | String        | O         | 


### Success Response Body Fields

Name              | Type(value)   | Mandatory | Description
------------------| --------------| ----------| -------------------
transactionId     | String        | M         | 
userAccount       | String        | M         | 
accountId         | String        | M         | 
currency          | String        | M         | 
transactionType   | String        | M         | Trade/Deposit/Withdraw/Fee/Rebate/Order/PendingWithdraw
amount            | DoubleString  | M         | 
balance           | DoubleString  | M         | 
available         | DoubleString  | M         | 
timestamp         | Timestamp     | M         | 
referenceId       | String        | M         | Additional information;Trade – {tradeId};Withdraw – {withdrawId};Fee – {tradeId or withdrawId};Order – {orderId};WithdrawRequest – {withdrawId}


### Failure Error Codes

Error Code            | Description      
----------------------| -----------------

<a name="withdraw" id="withdraw"> </a>

---
## Withdraw

POST /api/private/withdraw

### Request Parameters

Name            | Type(value)   | Mandatory | Description
----------------| --------------| ----------| -------------------
accountId       | String        | M         | 
amount          | String        | M         | 
address         | String        | M         | bankId or cryto address

### Success Response Body Fields

Name            | Type(value)   | Mandatory | Description
----------------| --------------| ----------| -------------------
withdrawId      | String        | M         | 

### Failure Error Codes

Error Code            | Description      
----------------------| -----------------
# Enums

* [orderStatus](#orderStatus)
* [timeInForce](#timeInForce)
* [side](#orderSide)
* [selfTradePrevention](#selfTradePrevention)
* [orderType](#orderType)
* [transactionType](#transactionType)
* [instrumentType](#instrumentType)
* [cancelReason](#cancelReason)

<a name="orderStatus" id="orderStatus"> </a>
## orderStatus

Order Status             | Description
-------------------------| ---------------------------------------
PENDING_NEW              | New order has been accepted
NEW                      | New order has been booked
PARTIAL_FILLED           | Order is partially filled
FILLED                   | Order is fully filled
PENDING_CANCEL           | Order cancel request has been accepted
CANCELLED                | Order has been cancelled and removed from book

<a name="timeInForce" id="timeInForce"> </a>
## timeInForce

Time in Force            | Description
-------------------------| ---------------------------------------
GTC                      | Good till cancelled orders remain in the book until cancelled or filled.
IOC                      | Immediate or cancel orders must be executed instantly and any unfilled parts of the order are cancelled.
FOK                      | Fill or kill orders are rejected if the entire size can not be matched.

<a name="side" id="side"> </a>
## side

Side                     | Description
-------------------------| --------------------------------------
BUY                      | Buy order indicator
SELL                     | Sell order indicator

<a name="selfTradePrevention" id="selfTradePrevention"> </a>
## selfTradePrevention

Self Trade Prevention    | Description
-------------------------| --------------------------------------
CO                       | Cancel older order in the book
CN                       | Cancel new order
CB                       | Cancel both orders

<a name="orderType" id="orderType"> </a>
## orderType

Order Type               | Description
-------------------------| -------------------------------------
LIMIT                    | Limit orders require specifying a price and size
MARKET                   | Market orders provide no pricing guarantees. They execute immediatly and no part of the market order will go on the orer book.
STOP_LOSS (TBA)          | A market order is placed when the last price moves to the value at or below the stop price.  The trade may happen at the worse price than stop price.
STOP_LOSS_LIMIT (TBA)    | A limit order is placed when the last price moves to the value at or below the stop price.
STOP_ENTRY (TBA)         | A market order is placed when the last price moves to the value at or above the stop price. The trade may happen at the worse price than stop price.
STOP_ENTRY_LIMIT (TBA)   | A limit order is placed when the last price moves to the value at or above the stop price.

<a name="transactionType" id="transactionType"> </a>
## transactionType

Transaction Type         | Description
-------------------------| --------------------------------------
DEPOSIT                  |
WITHDRAW                 |
BUY                      |
SELL                     |

<a name="instrumentType" id="instrumentType"> </a>
## instrumentType

Instrument Type          | Description
-------------------------| --------------------------------------
SPOT                     | 
FUTURES (TBA)            |

<a name="cancelReason" id="cancelReason"> </a>
## cancelReason

Cancel Reason            | Description
-------------------------| ---------------------------------------
USER_CANCEL              | The order is cancelled by user.
NO_LIQUIDITY             | Market order or IOC order cancelled remaining by system.
SELF_TRADE               | The order is cancelled due to self trade prevention.
POST_ONLY                | The post only order is taking liquidity, cancelled by system.
INSUFFICIENT_LIQUIDITY   | The FOK order cannot fully trade, cancelled by system.

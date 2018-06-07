# Error Codes

Error Code                              | Description
----------------------------------------| ---------------------------------------
EXCEED_BALANCE                          | Insufficient balance for the new order.
ALREADY_DONE                            | The order is already cancelled or fully filled.
ALREADY_PENDING_CANCEL                  | The order is already in pending cancel state.
INVALID_INSTRUMENT                      | The instrumentId is invalid or has been disabled
SIZE_LESS_THAN_MIN_SIZE                 | The order size is less than the minOrderSize of the instrument.
SIZE_MORE_THAN_MAX_SIZE                 | The order size is more than the maxOrderSize of the instrument.
SIZE_NOT_DIVISIBLE_BY_LOT_SIZE          | The order size is either too high or too low and not in the multiples of the instrument.
PRICE_NOT_DIVISIBLE_BY_TICK_SIZE        | The order price is not divisible by the tickSize of the instrument.
INVALID_ORDER_SIDE                      | The side is invalid.
INVALID_ORDER_STATUS                    | The orderStatus is invalid.
UNIQUE_ORDER_ID_REQUIRED                | Neither orderId nor clientOrderId is provided.
INVALID_INSTRUMENT_STATUS               | Request is not allowed in current instrument status.
QUOTE_AMOUNT_REQUIRED                   | The orderType is MARKET and side is BUY but quoteAmount is not provided.
SIZE_REQUIRED                           | The orderType is MARKET and side is SELL but size is not provided.
PRICE_LESS_THAN_MIN_PRICE               | The order price is less than the minOrderPrice of the instrument.
PRICE_MORE_THAN_MAX_PRICE               | The order price is more than the maxOrderPrice of the instrument.
API_BAD_REQUEST,                        | Bad request that contains either invalid fields or invalid field values
INTERNAL_SERVER_ERROR,                  | Internal server error.
API_CALL_UNAUTHORIZED,                  | The api call is not authenticated.
TWO_FACTOR_UNAUTHORIZED,                | Need two factor authentication.
INVALID_EMAIL_FORMAT,                   | The email provided by the user is valid.
INVALID_USERNAME_FORMAT,                | The user name provided by the user is invalid.
INVALID_REGISTRATION_CONFIRMATION_CODE, | User invalid confirm code.
INVALID_OLD_PASSWORD,                   | The password provided by user to reset password is invalid.
BAD_PASSWORD,                           | Password format dosen't meet the requirement.
EMAIL_IN_USE,                           | The email is registered by other user.
USERNAME_IN_USE,                        | The username is registered by other user.
USER_REGISTRATION_UNCONFIRMED,          | The user has registered but not confirmed.
USER_REGISTRATION_HAS_BEEN_CONFIRMED,   | The user has been confirmed already.
USER_DISABLED,                          | The user is disabled.
USER_AUTH_BAD_CREDENTIALS,              | The credentials provided by user is invalid.
PASSWORD_SAME_TO_PREVIOUS,              | Cannot set the password same to previous.
USER_NOT_EXIST,                         | Can't find the user with the auth token.
INVALID_USERACCOUNT_NAME_FORMAT,        | The user account name provided by user is invalid.
USERACCOUNT_NAME_IN_USE,                | The user account name has been taken.
USER_MAIN_ACCOUNT_DELETE_NOT_ALLOWED,   | Cannot delete the user main account.
USER_MAIN_ACCOUNT_HAS_EXISTED,          | Cannot create user main account cause the user already has one.
USERACCOUNT_DELETE_NOT_ALLOW,           | User account deletion is not allowed.
USERACCOUNT_DISABLED,                   | The user account is disabled.
USERACCOUNT_NOT_EXIST,                  | Can't find the user account with the provided credentials. 
APIKEY_NOT_EXIST,                       | Cannot find the apikey with the provided credentials.
APIKEY_DISABLED,                        | The apikey is disabled.
BAD_PASSCODE,                           | The apikey passcode is invalid.
INVALID_AUTHORITIES                     | The apikey authorities is invalid.




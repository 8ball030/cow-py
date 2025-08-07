# Orders

Functionality for creating and managing orders on the COW Protocol.

## Overview

The `orderbook_api` module provides functionality to create, manage, and interact with orders on the COW Protocol. It includes classes and methods for handling different types of orders, such as limit orders and market orders, as well as utilities for order management.



## Creating Orders

### Market Orders

Swapping tokens using market orders is straightforward. You can specify the amount of the token you want to sell, and the system will execute the swap at the best available market price.

```python
import os
import asyncio
from dotenv import load_dotenv
from web3 import Account, Web3
from web3.types import Wei
from cowdao_cowpy.cow.swap import swap_tokens
from cowdao_cowpy.common.chains import Chain

BUY_TOKEN = Web3.to_checksum_address(
    "0xfFf9976782d46CC05630D1f6eBAb18b2324d6B14"
)  # WETH
SELL_TOKEN = Web3.to_checksum_address(
    "0xbe72E441BF55620febc26715db68d3494213D8Cb"
)  # USDC
SELL_AMOUNT_BEFORE_FEE = Wei(5000000000000000000)  # 50 USDC with 18 decimals
CHAIN = Chain.SEPOLIA

load_dotenv()

PRIVATE_KEY = os.getenv("PRIVATE_KEY")

SLIPPAGE_TOLERANCE = 0.005  # 0.5% slippage tolerance
VALID_TO = datetime.datetime.now().timestamp() + 3600  # Valid for 1 hour

ACCOUNT = Account.from_key(PRIVATE_KEY)

# Execute the swap
# This will create a market order to swap SELL_TOKEN for BUY_TOKEN
asyncio.run(
    swap_tokens(
        amount=SELL_AMOUNT_BEFORE_FEE,
        account=ACCOUNT,
        chain=CHAIN,
        sell_token=SELL_TOKEN,
        buy_token=BUY_TOKEN,
        slippage_tolerance=SLIPPAGE_TOLERANCE,
        valid_to=int(VALID_TO),
    )
)

```


### Buying Tokens
To buy tokens using the CoW Protocol, you can create a market order that specifies the amount of tokens you want to purchase. The system will execute the order at the best available market price.

```python
# TODO: Implement buying tokens example
```

### Limit Orders

Limit orders allow you to specify the price at which you want to buy or sell a token. The order will only be executed if the market price reaches your specified limit price.

```python
# TODO: Implement limit order creation example
```


### Fetching Order Details

To fetch details about a specific order, you can use the `get_order` method. This method retrieves information about an order based on its ID.

```python
from cowdao_cowpy.order_book.api import OrderBookApi, UID

# Initialize the OrderBookApi
order_book_api = OrderBookApi()

# Fetch and display individual order details
order = order_book.get_order_by_uid(UID("0x..."))
print(order)

# Fetch all orders for a specific user

orders = order_book_api.get_orders_by_owner("0x...")

# Display all orders
for order in orders:
    print(order)

```
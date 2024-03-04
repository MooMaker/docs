# Market maker settles order with his own funds

## Actors
- Trader
- Market Maker

## Description
Use case explains how market makers can settle orders with their own funds.

## Preconditions
- Market maker has enough amount of tokens user wants to buy.
- 1 ETH = 1000 USDC

| Token / Balance | Market Maker | Trader |
|-----------------|:------------:|:------:|
| ETH             |      1       |   0    |
| USDC            |      0       |  1000  |

## Trigger
User places an order to buy ETH.

## Main flow
- Trader posts an order to buy tokens (e.g. ETH for USDC)
- Maker wins auction
- Maker sends funds directly to the trader
- Trader sends funds directly to the maker

## Alternative flows
### Market maker partially fills order 
In this case we need a extra makers to fill the rest of the order.

### Order is canceled
Auction stops

## Postconditions
| Token / Balance | Market Maker |   Trader   | System |
|-----------------|:------------:|:----------:|:------:|
| ETH             |      0       | 1 - fees % | fees % |
| USDC            |     1000     |     0      |   0    |

## Exceptions

### No makers matched the order
Order times out

## Use case diagram
```mermaid
flowchart LR
    subgraph Settle order with own funds
        uc0((Place order))
        uc1((Trade tokens))
        uc2((Settle order))
    end
    
    trader[Trader]
    mm[Market Maker]
    
    trader ----> uc0
    trader ----> uc1
    mm ----> uc1
    mm ----> uc2
    
    uc1 -. Include .-> uc2
    uc1 -. Include .-> uc0
```


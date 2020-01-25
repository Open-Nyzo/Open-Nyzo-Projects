# Open DB Analysis

Nyzo Blockchain as a DB. 

This concerns the DB structure and Storage itself.  
Engines that would write/feed into this DB - as well as client apps that would read from it - are a separate thing, to be referenced here anyway.

## A. Goals

- Store all Nyzo blockchain data since genesis
- Use a known db engine, with available bindings in all common languages
- Index main transactions and block fields for lookups
- Be optimized for minimal storage space
- Non nonsense structure
- Documented

## B. Possible uses

### B1. Explorer  

- Get balances of addresses
- Get latest blocks
- Get latest transactions
- Lookup transactions by address (sender/recipient)
- Lookup transactions by block height
- Lookup transactions by txid (=signature?)

### B2. dApps

- Query transactions by recipient
- Query transactions by data
- Limit to some block range

## C. Potential DB Feeder apps

- Monk's Go implementation
- Potential Jyson/nyzo client feeder by Eggdrasyl
- 

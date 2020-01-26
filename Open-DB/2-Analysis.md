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

## B. Possible uses

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

### B3. Bitcoin like Json/RPC interface

WIP - requirements in terms of data/requests to be added.

### B4. Cycle events logging

Maintain a searchable history of cycle events for future analysis and anomalies detection.  
cycle info, votes, joins, leaves

### B5. Exchange

Similar to B3. Exchanges are used to bitcoin like json-rpc.  
They need to  
- query last txns for an address
- get a txid for a txn they sent
- lookup a txn from its txid
- get list txs from block X , optionally filter out by recipient (can monitor a large number of recipients if one wallet per user)
- query balances

### B6. Online shop

Similar to B5 and B3.  
Need a way to get an event when a transaction to them has been made and is safe to honor.

### B7. Layer 2 protocol

See Bismuth Abstract transactions.  
Uses data field to support custom protocol (like NFTs, FTs, dApps)

Needs B5/B3 + more complex queries on data fields.  
Like, all txns from block #N whose data matches "tk:??:xx"

### B8. Nyzo service provider

Automated Online service, providing something in exchange for a nyzo payment, with potentially data in the txn
- similar to B6  
- may need lookups on data, if implements a layer 2 protocol like B7

## C. Potential DB Feeder apps

- Monk's Go implementation
- Potential Jyson/nyzo client feeder by Eggdrasyl
- 

## D. Open questions/concerns

- space/computation arbitrage. Fees/Balances/votes history ?
- cycles txns?

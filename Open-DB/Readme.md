# Nyzo Open DB

## Goal

Have the Nyzo blockchain data under an open DB format that external tools can access and query.  
To be used as backend for next gen explorers, rpc servers, dApps API...

Lots of work went behind the scenes involving Monk, Iyomisc and EggPool.   
A relationnal database structure was defined to store and index blocks, transactions as well as cycle events.

This database is used as a common structure able to represent the whole state of the current Nyzo blockchain.  
This is just a database.  
Tools to extract data from this database are listed one level above, for instance https://github.com/Open-Nyzo/Open-Nyzo-Projects/blob/master/Wallet_servers.

Tools that read nyzoblocks and/or query the network and can feed historical and/or live data into that DB are called "DB-Feeder"s.

## State

4 - Development and Implementation

Current structure is specified at https://github.com/Open-Nyzo/Open-Nyzo-Projects/blob/master/Open-DB/open-db-structure.md

## Contributions and Implementations

- Monk and EggPool: Definition of the initial DB structure  
- Monk: Prototype of a sentinel implementation in Golang.  
  Able to digest nyzoblocks and stay sync with the frozen edge, fully validating the chain.  
  Uses the open db as core data format.  
  Not public nor released atm, release as open source is planned in the future.
- Iyomisc: prototype of a python feeder and tracker, able to read historical nyzoblocks then stay sync with the live chain, storing chain data into the open db.  
  Used as data source for the explorer at https://nyzo.today/explorer/.
  Explorer is public, code was not release as for now, may be open sourced later on.


## Contributors

You are welcome to list your competences and how you'd like to help, just PR to [Contributors list](../contributors.md).

## Suggestions and future ideas

From @x00x0x00x: concerns and proposals about bootstrapping a new DB instance.

Current source consists of consolidated nyzoblocks provided and hosted by the core devs.  
These are encoded under a documented format, and could be one safe reference, with hash of consolidated files being published on the chain by authorities sources (protocol to be specified).

Another way of ensuring a bootstrap file is correct is by comparing the balance list - which contains balances but also cycle votes - at a given height.

Another data source could then be a raw sql export of the open db itself, or read only access to a sql instance.  
Such access could optionally be offered for a fee by existing db holders, given an integrity check protocol exists.


To be moved to ../wallet_servers:

- [**full-node-lightwallet-sync.md by x00x0x00x**: ](full-node-lightwallet-sync.md): agreed standard for light-wallet developers and full node operators || methods, efficiency, setup procedure

# Commands

This are the commands any open nyzo compatible implementation has to provide.

Whenever possible, command and parameter names follow bitcoin standards and behaviour.  
They are not bound to a specific development language or transport layer.
https://github.com/EggPool/Jyzon/blob/master/commands.md  can be used as reference (common points and differences with bitcoin rpc server)

WIP

## Minimal command set

These commands allow for minimal light wallet operation.

### getinfo
Returns an object containing various state info.

Example:
```
```

### getbalancebyaddress - (nyzo address, raw or id_)

Returns the total balance of the given address.  


### getaddresssince - (block_height) (nyzo address)

Returns the transactions matching the given address, following a given block_height.
Returns at most info from 720 blocks (the older ones)  

This allows to query all transaction history for an address by successive calls, and go on from latest known state on a further run.

### listtransactions - (nyzo_address) (count=10) (from=0)

Returns up to (count) most recent transactions skipping the first (from) transactions for address (nyzo_address).  
If (nyzo_address) is not provided it'll return recent transactions from all addresses.

### counttransactions - (nyzo_address)

Returns the number of known transactions for (nyzo_address)

### getblocksince - (block_height)

Returns the full blocks (with all transactions) following a given block_height  
Returns at most 10 blocks (the older ones)  
Used by client apps to keep track and be notified of new tx for many addresses at once.

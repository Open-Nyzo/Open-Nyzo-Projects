# Engine

MySql/MariaDB relational database was chosen.  

Since blocks and transactions use a fixed structure, this gives greater control on field types, storage and indices as well as more complex queries.

The same strcuture can be used almost as-is with other sql engines, and should be almost directly translatable to a document oriented database if that was needed for a reason.

# Structure

Credits go to Monk, Iyomisc, EggPool.

## Transactions

```CREATE TABLE IF NOT EXISTS transactions (
  height bigint(20) NOT NULL,
  canonical int(11) NOT NULL,
  timestamp bigint(20) NOT NULL,
  type tinyint(4) NOT NULL,
  sender binary(32) DEFAULT NULL,
  recipient binary(32) NOT NULL,
  data binary(32) DEFAULT NULL,
  amount bigint(20) NOT NULL,
  amount_after_fees bigint(20) NOT NULL,
  sender_balance bigint(20) DEFAULT NULL,
  recipient_balance bigint(20) NOT NULL,
  signature binary(64) DEFAULT NULL,
  vote tinyint(3) unsigned DEFAULT NULL,
  original_signature binary(64) DEFAULT NULL,
  PRIMARY KEY (height,canonical),
  KEY sender (sender(4)),
  KEY recipient (recipient(4)),```

Stores the individual transactions.  
- `height` is the matching block height
- `canonical` is the transaction index in the block
- Hashs, identifiers and signature are stored as binary
- Amounts are stored as int, that is amount of micronyzos.
- `sender_balance` and `recipient_balance` are the balances after the transaction is applied.
- `vote` and `original_signature` are null unless transaction type is 4

> Note: Sender and recipient balance denormalization at transaction level ease up balance calculations, without requiring full balance list to be stored every block.  
Some implementations may not use these fields and leave them Null


## Blocks

The blocks themselve.

```CREATE TABLE IF NOT EXISTS blocks (
        chain_version SMALLINT SIGNED NOT NULL,
        height BIGINT SIGNED NOT NULL,
        hash BINARY(32) NOT NULL,
        previous_hash BINARY(32) NOT NULL,
        cycle_length INT SIGNED NOT NULL,
        start BIGINT SIGNED NOT NULL,
        verification BIGINT SIGNED NOT NULL,
        transaction_count INT SIGNED NOT NULL,
        balance_list_hash BINARY(32) NOT NULL,
        verifier BINARY(32) NOT NULL,
        signature BINARY(64) NOT NULL,
        PRIMARY KEY (height))```

## Cycle events

Stores all cycle changes.  

```
CREATE TABLE IF NOT EXISTS cycle_events (
  height bigint(20) NOT NULL,
  identifier binary(32) NOT NULL,
  joined tinyint(1) NOT NULL,
  PRIMARY KEY (height,identifier)
)
```

joined is `true` is `identifier` joined the cycle, `false` if it left it.


## Optional indices

Structure above contains the minimal indices needed for a working and minimal database.

More indices can be added to accelerate common requests.  
These are left to the requester goodwill.

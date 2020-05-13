# Engine

MySql/MariaDB relational database was chosen.  

Since blocks and transactions use a fixed structure, this gives greater control on field types, storage and indices as well as more complex queries.

The same structure can be used almost as-is with other sql engines, and should be almost directly translatable to a document oriented database if that was needed for a reason.

# Structure

Credits go to Monk, Iyomisc, EggPool.

## Transactions

```
CREATE TABLE IF NOT EXISTS transactions (
  height bigint(20) NOT NULL,
  canonical int(11) NOT NULL,
  timestamp bigint(20) NOT NULL,
  type tinyint(4) NOT NULL,
  sender binary(32) DEFAULT NULL,
  recipient binary(32) DEFAULT NULL,
  data binary(32) DEFAULT NULL,
  amount bigint(20) DEFAULT NULL,
  amount_after_fees bigint(20) DEFAULT NULL,
  sender_balance bigint(20) DEFAULT NULL,
  recipient_balance bigint(20) DEFAULT NULL,
  signature binary(64) DEFAULT NULL,
  vote tinyint(3) unsigned DEFAULT NULL,
  original_signature binary(64) DEFAULT NULL,
  PRIMARY KEY (height,canonical),
  KEY sender (sender(4)),
  KEY recipient (recipient(4)),
  KEY timestamp (timestamp),
  KEY signature (signature(4)),
  KEY original_signature (original_signature(4)),
  KEY type (type))
```

Stores the individual transactions.  
- `height` is the matching block height
- `canonical` is the transaction index in the block
- Hashs, identifiers and signature are stored as binary
- Amounts are stored as int, that is amount of micronyzos.
- `sender_balance` and `recipient_balance` are the balances after the transaction is applied.
- `vote` and `original_signature` are null unless transaction type is 4

Cycle transactions:
- V1 blockchain: cycle transactions are tracked off chain, stored in DB once accepted (once they appeared in a block)
- V2 blockchain: cycle transactions are stored twice, on creation, with sender_balance and recipient_balance both set to NULL, then again on acceptance with the correct balances

> Note: Sender and recipient balance denormalization at transaction level ease up balance calculations, without requiring full balance list to be stored every block.  
Some implementations may not use these fields and leave them Null


## Blocks

The blocks themselve.

```
CREATE TABLE IF NOT EXISTS blocks (
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
  PRIMARY KEY (height),
  KEY hash (hash(4)),
  KEY signature (signature(4)))
```

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

## Node status

Node status information.

```
CREATE TABLE node_status1 (
  identifier binary(32) NOT NULL,
  timestamp bigint(20) NOT NULL,
  ip binary(4) NOT NULL,
  nickname varchar(32) COLLATE utf8mb4_unicode_ci NOT NULL,
  version int(11) NOT NULL,
  mesh_total int(11) NOT NULL,
  mesh_cycle int(11) NOT NULL,
  cycle_length int(11) NOT NULL,
  transactions int(11) NOT NULL,
  retention_edge bigint(20) NOT NULL,
  trailing_edge bigint(20) NOT NULL,
  frozen_edge bigint(20) NOT NULL,
  open_edge bigint(20) NOT NULL,
  blocks_transmitted bigint(20) NOT NULL,
  blocks_created bigint(20) NOT NULL,
  vote_stats varchar(1024) COLLATE utf8mb4_unicode_ci NOT NULL,
  last_join_height bigint(20) NOT NULL,
  last_removal_height bigint(20) NOT NULL,
  receiving_udp tinyint(4) NOT NULL,
  PRIMARY KEY (ip,identifier,nickname)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

Observe the CHARSET specifications for this table, a default table creation will not work, as default "utf8" as implemented by MySQL is not compatible with the emojis some people use in their verifier nicknames.

The table is primkeyed by ip, identifier, nickname, so any change of the IP or nickname will leave back a historical data entry in the table in case somebody wants to know historical IPs or nicks for individual node identifiers. 
# Transakzioak

- Transakzio bat eragiketa multzo bat da, guztiek lortzen (commit) dutena edo denek huts egiten dutena (rollback).
- ACID betetzen dute:
  - Atomicity: 100 edo 0
  - Consistency: hasieran eta amaieran datuen trinkotasun arauak errespetatu behar dira
  - Isolation: batera martxan dauden transakzioak ezin dute beste transakzio baten bitarteko aldaketak ikusi
  - Durability: emaitzak betirako mantentzen dira

## Race conditions

- Dirty reads: Reading data that has been modified but not yet committed by another transaction
- Dirty writes: One transaction overwrites data written by another transaction that hasn’t committed yet
- Read skew/non repeatable reads: A transaction reads the same data twice and gets different values because another transaction modified it in between
- Lost updates: Two transactions update the same data, and one update overwrites the other
- Write skew: Two transactions read the same data and then update different parts of it, causing a constraint violation
- Phantom reads: A transaction re-executes a query and gets a different set of rows because another transaction inserted or deleted data

## Transkazio mailak

- Read uncommitted: Transactions can see uncommitted changes from others
- Read committed: Transactions only see committed data
- Repeatable read: Once a row is read, it cannot change during the transaction
- Serializable transactions: Transactions behave as if executed one after another (no concurrency issues)

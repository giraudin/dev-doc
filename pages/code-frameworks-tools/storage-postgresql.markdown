---
layout: page
title: PostgreSQL
permalink: /storage-posgresql/
---

## Resources
- [https://www.postgresql.org/docs/current/](https://www.postgresql.org/docs/current/){:target="_blank"}
- [WAL Introduction](https://www.postgresql.org/docs/current/wal-intro.html){:target="_blank"}
- [https://github.com/zalando/spilo](https://github.com/zalando/spilo){:target="_blank"}
- [https://github.com/zalando/patroni](https://github.com/zalando/patroni){:target="_blank"}
- [https://wiki.postgresql.org/wiki/Replication,_Clustering,_and_Connection_Pooling](https://wiki.postgresql.org/wiki/Replication,_Clustering,_and_Connection_Pooling){:target="_blank"}
- [https://hub.docker.com/postgres](https://hub.docker.com/_/postgres/){:target="_blank"}


## Objective
The aim is to add, as a starting point in the dev env (docker containers), a High Availability PorstgreSQL cluster with replication, load balancing and failover.
This whould consist in a Master (primary) for the write operations and 2 secondaries(standby)  with load balancing for the read only operations.


### Available strategies
There are several available strategies for different scenarios: [comparison of different solutions](https://www.postgresql.org/docs/current/different-replication-solutions.html){:target="_blank"}


### Key points for the first experimentations
- Synchrone replication (less asynchrone as possible).
- Minimal risk of data loss.
- Service level replication: no Shared Disk Failover but File System Replication (see [DRDB](https://fr.wikipedia.org/wiki/DRBD){:target="_blank"}) could be used as a failover solution but not for replication.
- Keep as simple as possible : replication of the entire database, no data partitioning (i.e.: tables splitted into set)  and consequently no Parallel Query Execution.
- No risk of data loss: discard Trigger-Based Primary-Standby Replication as according to the documentation "there is possible data loss during fail over".
- Hot secondaries: the replication need to be synchronous for the load balancing.
- Transparent: no adaptation of the code or queries to the used strategy. This discard the SQL-Based Replication Middleware, adapation of function like CURRENT_TIMESTAMP and transactions must be managed for all servers independently.
- No multi masters.

### Tested strategy
The first tested strategy is Write-Ahead Log Shipping. 
In a second step, Logical Replication (table level replication) and Synchronous Multimaster Replication could be tested. NB: This is not implemented directly in Postgres, it has to be implemented in the app code.
In a third step, we could experiment Data Partitioning and Multiple-Server Parallel Query Execution.

### Write-Ahead Log Shipping
Two implementations: [Log-Shipping](https://www.postgresql.org/docs/current/warm-standby.html) and [Streaming Replication](https://www.postgresql.org/docs/current/warm-standby.html#STREAMING-REPLICATION). The last one will be used as there is less latency.


#### Streaming replication
- Principle: [WALL](https://www.postgresql.org/docs/current/wal-intro.html){:target="_blank"} replication
- Small delay (smaller than with log-shipping)
- archive_timout not required (data loss window)
- **wal_keep_size** this has to be set carrefully (large enough): **if WAL segment are recycled to quickly, the standby server has to be reinitialized.**


---
layout: page
title: PostgreSQL
permalink: /storage-posgresql/
---

## Objective
The aim is to add, as a starting point in the dev env (docker containers), a High Availability PorstgreSQL cluster.
This whould consist in a Master (primary) for the write operations and 2 secondaries with load balancing for the read only operations.

### Available strategies
There are several available strategies for different scenarios: [comparison of different solutions](https://www.postgresql.org/docs/current/different-replication-solutions.html){:target="_blank"}


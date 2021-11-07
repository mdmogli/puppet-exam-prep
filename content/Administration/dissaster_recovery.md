# Disaster Recovery

[INDEX](../../README.md)

### Overview:

Disaster recovery creates a replica of your primary server. You can have only one replica at a time, and you can add disaster recovery to an installation with or without compilers. Disaster recovery isn't supported with standalone PE-PostgreSQL or FIPS-compliant installations.

There are two main advantages to enabling disaster recovery:

- If your primary server fails, the replica takes over.
- If your primary server can’t be repaired, you can promote the replica to primary server.

The replica is not an exact copy of the primary server. Rather, the replica duplicates specific infrastructure components and services. Hiera data and other custom configurations are not replicated.

Replication can be read-write or read-only and Failover is automatic.
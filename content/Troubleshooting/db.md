# Troubleshooting PosgreSQL

## Overview
If you have issues with the databases that support the console, make sure that the PostgreSQL database is not too large or using too much memory.

### PosgreSQL is taking much space
The PostgreSQL autovacuum=on setting prevents the database from growing large.

### PosgreSQL is taking much memory
Error is present in /var/log/pe-postgresql/pgstartup.log.

```bash
$ sysctl -w kernel.shmmax=<your shmmax calculation>
$ sysctl -w kernel.shmall=<your shmall calculation>
```

### PuppetDB conflicts port 

By default, PuppetDB communicates over port 8081, check if other service is using it.

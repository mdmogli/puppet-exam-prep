# Troubleshooting HA

## Overview
If disaster recovery commands fail, check for these issues.

### Latency over WAN
if you have a high latency comm path between primary and replica, try re-run the command again.

### Replica is connected to a compiler instead of a primary server
On the replica you want to provision, edit /etc/puppetlabs/puppet.conf so that the server and server_list settings use a primary server, rather than a compiler.


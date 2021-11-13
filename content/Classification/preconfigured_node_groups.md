# Preconfigured node groups

[INDEX](../../README.md)

## Pre defined node groups:

### All Nodes node group:
Top of the hierarchy tree, All other node groups stem from this:

1. Non default classes, puppet_enterprise.
1. matching all nodes, cannot be modified.

### PE Infrastructure node group:
Parent of Puppet infra nodes.

1. default classes, puppet_enterprise.
1. No matching nodes, never pin nodes here.

#### PE Certificate Authority:
to manage the certificate authority.

1. puppet_enterprise::profile::certificate_authority
1. fresh install only primary node is pinned.
   
#### PE Master:
To manage the primary server

1. puppet_enterprise::profile::master
2. fresh install only primary is pinned.

#### PE Compiler:
Subset of the PE Master to manage compilers.

1. puppet_enterprise::profile::master & puppet_enterprise::profile::puppetdb

#### PE Orchestator
to manage PE orchestation services.

1. puppet_enterprise::profile::orchestrator
2. fresh install only primary node is pinned.
   
#### PE PuppetDB
Nodes running the PuppetDB service

1. puppet_enterprise::profile::puppetdb
2. nodes that aren't act as a compilers are pinned here.

#### PE Console
to manage the console.

1. puppet_enterprise::profile::console & puppet_enterprise::license
   
#### PE Agent
to manage the configuration of agents.

1. puppet_enterprise::profile::agent
2. All managed nodes are pinned to this group.

#### PE Infrastructure Agent
Subset of PE Agent, to manage infrastructure-specific overrides.

1. puppet_enterprise::profile::agent
2. Puppet infrastructure and managed by the PE installer are pinned.

#### PE Database
to manage the PostgreSQL.

1. puppet_enterprise::profile::database

#### PE Patch Management node group
For nodes under patch management.

1. pe_patch class.
2. no nodes pinned to this group by default.
# Puppet Architecture

[INDEX](../../README.md)

## Primary server and compilers:

- Puppet server (runs on primary & compilers): host endpoints for the certificate authority service and powers the catalog compiler.
  - Catalog compiler: to enforce a server, this server uses a catalog. This catalog is compiled by puppet server and has the desire state.
- File sync (server in primary and client mode on compiler): keeps your code synchronized across multiple compilers.
- Certificate Authority (Primary): Accepts certificate signing requests (CSRs) from nodes, serves certificates and a certificate revocation list (CRL) to nodes, and optionally accepts commands to sign or revoke certificates.
- Console service (primary): 
  - The console: Web console.
  - RBAC: mangage permissions to users and groups, LDAP connections, AD connections.
  - Node Classifier: Apply classes to managed nodes, specified values and seetings to specific nodes.
- Code Manager and r10k (Primary): Manage and sync enviroments based on branches defined on GIT.
- Orchestation service (Primary): Manage on-demand/scheduled puppet agents runs, tasks and plans.
- PuppetDB: Service that collects data from managed servers, allows exported resources. Store agent reports.
- PE databases (Primary or splited):
  - pe-puppetdb: Exported resources, catalogs, facts, and reports.
  - pe-activity: Activity data from the Classifier, including who, what and when.
  - pe-classifier: Classification data, all node group information.
  - pe-rbac: Users, permissions, and AD/LDAP info.
  - pe-orchestrator: Details about job runs, users, nodes, and run results
  
## Architecture options:

- Standard installation: Primary server (Replica optional) without the use of compilers.
- large installation: Primary server (Replica optional) with compilers.
- extra-large installation: Primary server (Replica optional) with compilers and splitted database server (PE-Database services).
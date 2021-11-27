# Running Jobs from CLI

[INDEX](../../README.md)

## Overview:
Puppet runs every 30min by default, Use the puppet job run command to enforce change on your agent nodes. In order to use this featur PE infra is needed.

You can run jobs on three types of targets, but these targets cannot be combined:

- A list of nodes or a single node
- A node group
- A PQL nodes query

When you execute a puppet job run command and compiles a new catalog for all nodes included in the job.

You can use the following options:
* --noop: dry run
* --no-nopp: overrides any noop in the agent
* --environment, -e: defines the env
* --no-enforce-environment: ignore env for agent.
* --description: description for the job.
* --concurrency: default unlimited.

### Examples:

```bash

    # run a job on a list of nodes
    $ puppet job run --nodes node1,node2 <options>

    # using a list
    $ puppet job run --nodes @/path/to/file.txt <options>

    # using PQL
    $ puppet job run --query 'nodes { certname = "mynode" }' <options>

    # usign a node group
    $ puppet job run --node-group <node-group-id> <options>

```

1. PXP: A message format used to request that a task be executed on a remote host and receive responses on the status of that task.
2. PXP agent: Service in the agent that runs PXP.
3. PCP: The underlying communication protocol.
4. PCP brokers: route PCP messages. Compilers are connected to primary and angents connected through compilers use these as a proxy.

### Workflows
#### puppet job command workflow:
1. User creates a job using CLI or Console.
2. Orchestator validates the token.
3. Orchestrator request env classification and query PuppetDB for nodes.
4. Orchestrator creates a jobid and start polling the status of nodes.
5. Orchestrator query puppetDB for puppet agent version.
6. Orchestrator tells PCP broker to start runs.
7. Agents sends results to PCP broker.

#### puppet task command workflow:
1. Client send a task command.
2. Orchestator validates if user is auth.
3. Orchestrator query PuppetDB for nodes.
4. Orchestrator requests task data from Puppet Server.
5. Orchestrator validates task command and send jobid to client.
1. Orchestrator seddn task data to the PXP agent.
6. The task runs.
7. The PXP agent sends the result to the orchestrator.

### Important config path

- pe-orchestration-services: /etc/puppetlabs/orchestration-services/conf.d
- PCP broker: /etc/puppetlabs/puppetserver/conf.d
- PXP agent: Configuration is managed by the agent profile (puppet_enterprise::profile::agent)
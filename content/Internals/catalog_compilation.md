# Catalog compilation

[INDEX](../../README.md)

## Overview:
When configuring a node, the agent uses a document called a catalog, which it downloads from the primary server. For each resource under management, the catalog describes its desired state and can specify ordered dependency information.

Puppet manifests are concise because they can express variation between nodes with conditional logic, templates, and functions. Puppet resolves these on the primary server and gives the agent a specific catalog.

### This allows Puppet to:

1. Separate privileges, because each node receives only its own resources.
1. Reduce the agent’s CPU and memory consumption.
1. Simulate changes by running the agent in no-op mode, checking the agent's current state and reporting what would have changed without making any changes.
1. Query PuppetDB for information about managed resources on any node.

**Note**: The puppet apply command compiles the catalog on its own node and then applies it.

### Puppet compiles a catalog using three sources of configuration information:

1. Agent-provided data: The node's name, The node's certificate, The node's facts, etc.
1. External data: Data from an external node classifier (ENC) or other node terminus, Exported resources, results of functions.
1. Manifests and modules, including associated templates and file sources

### The catalog compilation process

1. Retrieve the node object: by default it returns a black object from node terminus.
2. Set variables from the node object, from facts, and from the certificate: The node’s facts are set as top-scope variables.
3. Evaluate the main manifest: f there are node definitions in the manifest, Puppet must find one that matches the node’s name. If Puppet cannot find a match, it fails compilation.
4. Load and evaluate classes from modules.
5. Evaluate classes from the node object.

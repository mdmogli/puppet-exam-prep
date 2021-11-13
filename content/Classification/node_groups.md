# Classification and environment node groups

[INDEX](../../README.md)

## Two main types of node groups:

### Classification node groups:
Configure nodes by assigning classes, parameters, and variables to them. 

1. You can override variables from web console in the "Configuration" tab.
1. In the data section, you can override paramester from parent class definition.
1. In the variables tab, you can set up global variables.  

### Environments node groups:
Configure nodes by assigning environments (git branches) to them.

1. Must be a direct child of the All Environments node group
1. Must not include child groups, except any one-time run exception subgroups used for canary testing
1. Must be specified as an environment group in the group metadata
1. Must not include classes or configuration data

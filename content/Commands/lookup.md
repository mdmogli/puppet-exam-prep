# puppet lookup

[INDEX](../../README.md)

## Overview:
Does Hiera lookups from the command line. Since this command needs access to your Hiera data, make sure to run it on a node that has a copy of that data.

## Examples

```bash
# To look up 'key_name'
$  puppet lookup key_name

# look up 'key_name' with agent.local's facts
$ puppet lookup --node agent.local key_name

# lookup 'key_name' with agent.local's facts, and return a default value of 'bar' if nothing was found
$ puppet lookup --node agent.local --default bar key_name

# To see an explanation of how the value for 'key_name' would be found
$ puppet lookup --node agent.local --explain key_name
```
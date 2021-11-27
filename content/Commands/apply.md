# puppet apply

[INDEX](../../README.md)

## Overview:
Compiles, manages and apply configurations on nodes.

## Examples

```bash
# Apply a manifest and send logs to a file
$ puppet apply -l /tmp/manifest.log manifest.pp

# Apply a class and set the module path to a specific location
$ puppet apply --modulepath=/root/dev/modules -e "include ntpd::server"

# Apply a json catalog
$ puppet apply --catalog catalog.json
```
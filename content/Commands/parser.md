# puppet parser

[INDEX](../../README.md)

## Overview:
Validates a puppet manifest file.

## Examples:

```bash
# Validate the default site manifest at /etc/puppetlabs/puppet/manifests/site.pp:
$ puppet parser validate

# Validate two arbitrary manifest files:
$ puppet parser validate init.pp vhost.pp

# Validate from STDIN:
$ cat init.pp | puppet parser validate
```
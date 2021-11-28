# Hiera

[INDEX](../../README.md)

## Overview:
Puppet uses Hiera to do two things:
1. Store the configuration data in key-value pairs
2. Look up what data a particular module needs for a given node during catalog compilation

Puppet 5 and above comes with support for JSON, YAML, and EYAML files.

## Hiera hierarchy using static and dynamic pattern (facts):

```yaml
---
version: 5
defaults:  # Used for any hierarchy level that omits these keys.
  datadir: data         # This path is relative to hiera.yaml's directory. Ex: ./data dir location.
  data_hash: yaml_data  # Use the built-in YAML backend.

hierarchy:
  - name: "Per-node data"                   # Human-readable name.
    path: "nodes/%{trusted.certname}.yaml"  # File path, relative to datadir.
                                   # ^^^ IMPORTANT: include the file extension!

  - name: "Per-datacenter business group data" # Uses custom facts.
    path: "location/%{facts.whereami}/%{facts.group}.yaml"

  - name: "Global business group data"
    path: "groups/%{facts.group}.yaml"

  # Using eyaml for encrypted data
  - name: "Per-datacenter secret data (encrypted)"
    lookup_key: eyaml_lookup_key   # Uses non-default backend.
    path: "secrets/%{facts.whereami}.eyaml"
    options:
      pkcs7_private_key: /etc/puppetlabs/puppet/eyaml/private_key.pkcs7.pem
      pkcs7_public_key:  /etc/puppetlabs/puppet/eyaml/public_key.pkcs7.pem

  - name: "Per-OS defaults"
    path: "os/%{facts.os.family}.yaml"
  
  # Using several paths with "paths" option
  - name: "Per-OS defaults"
    paths: 
      - mix/file1.yaml
      - mix/file1.yaml

  - name: "Common data"
    path: "common.yaml"
```

## Using hiera within your puppet code

The lookup function:
- lookup( NAME, [VALUE TYPE], [MERGE BEHAVIOR], [DEFAULT VALUE] )
- lookup( [NAME], OPTIONS HASH )
- lookup( as above ) |$key| { VALUE } # lambda returns a default value

### Using the lookup function within puppet code:

```python
# Setting a default value if hiera doesn't find the variable
lookup('some::key', undef, undef, 'the default value')

# setting a variable type and changing merge behavior.
lookup('some::myarray', Array, unique)
```

```bash
$ puppet lookup KEY --node NAME --environment ENV --explain
$ puppet lookup --node agent.local key_name

# Changing the merge behavior (See Merge Behavior section)
$ puppet lookup --node agent.local key_name --merge unique
```

### Access hash array elements keysubkey notation
```yaml
accounts::users:
  ubuntu:
    home: '/var/local/home/ubuntu'
```
```python
lookup('accounts::users.ubuntu.home')
```

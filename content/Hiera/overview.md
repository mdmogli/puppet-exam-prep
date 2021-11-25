# Hiera

[INDEX](../../README.md)

## Overview:
Puppet uses Hiera to do two things:
1. Store the configuration data in key-value pairs
2. Look up what data a particular module needs for a given node during catalog compilation

Puppet 5 comes with support for JSON, YAML, and EYAML files.

## Hiera hierarchy:

```yaml
---
version: 5
defaults:  # Used for any hierarchy level that omits these keys.
  datadir: data         # This path is relative to hiera.yaml's directory.
  data_hash: yaml_data  # Use the built-in YAML backend.

hierarchy:
  - name: "Per-node data"                   # Human-readable name.
    path: "nodes/%{trusted.certname}.yaml"  # File path, relative to datadir.
                                   # ^^^ IMPORTANT: include the file extension!

  - name: "Per-datacenter business group data" # Uses custom facts.
    path: "location/%{facts.whereami}/%{facts.group}.yaml"

  - name: "Global business group data"
    path: "groups/%{facts.group}.yaml"

  - name: "Per-datacenter secret data (encrypted)"
    lookup_key: eyaml_lookup_key   # Uses non-default backend.
    path: "secrets/%{facts.whereami}.eyaml"
    options:
      pkcs7_private_key: /etc/puppetlabs/puppet/eyaml/private_key.pkcs7.pem
      pkcs7_public_key:  /etc/puppetlabs/puppet/eyaml/public_key.pkcs7.pem

  - name: "Per-OS defaults"
    path: "os/%{facts.os.family}.yaml"

  - name: "Common data"
    path: "common.yaml"
```

## Layered hierarchies 
Hiera uses layers of data with a hiera.yaml for each layer. A lookup works as following:

- global → environment → module.

### 1- Global layer:
is located, by default, in: $confdir/hiera.yaml

### 2- Environment layer:
is located, by default, in ENVIRONMENT DIR/hiera.yaml

### 3- Module layer:
is located, by default, in MODULE/hiera.yaml.

## Merge behaviors:
There are four merge behaviors to choose from: first, unique, hash, and deep.

### First:
A first-found lookup doesn’t merge anything: it returns the first value found for the key, and ignores the rest. This is **Hiera’s default behavior**.

## Looking up data from hiera:

When looking up a key, Hiera searches up to four hierarchy layers of data, in the following order:

1. Global hierarchy.
1. The current environment's hierarchy.
1. The indicated module's hierarchy, if the key is of the form MODULE NAME::SOMETHING.
1. If not found and the module's hierarchy has a default_hierarchy entry in its hiera.yaml — the lookup is repeated if steps 1-3 did not produce a value.

You can combine these arguments in the following ways:
- lookup( NAME, [VALUE TYPE], [MERGE BEHAVIOR], [DEFAULT VALUE] )
- lookup( [NAME], OPTIONS HASH )
- lookup( as above ) |$key| { VALUE } # lambda returns a default value

### Using the lookup function within puppet code:

```python
lookup('some::key', undef, undef, 'the default value')
```

```bash
$ puppet lookup KEY --node NAME --environment ENV --explain
$ puppet lookup --node agent.local key_name
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
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

## Class parameters: hiera vs params.pp

### params.pp pattern (deprecated)
The params.pp pattern takes advantage of the Puppet class inheritance behavior. It is a class that do nothing but set variables for other classes, The rest of the classes in the module inherit from the params class.

An example params class:
```python
# ntp/manifests/params.pp
class ntp::params {
  $autoupdate = false,
  $default_service_name = 'ntpd',

  case $facts['os']['family'] {
    'Debian': {
      $service_name = 'ntp'
    }
    'RedHat': {
      $service_name = $default_service_name
    }
  }
}
```

A class that inherits from the params class and uses it to set default parameter values:
```python
class ntp (
  $autoupdate   = $ntp::params::autoupdate,
  $service_name = $ntp::params::service_name,
) inherits ntp::params {
 ...
}
```

### hiera pattern
In this case, we use hiera to grab the values of the variables without using a class. Puppet can grab these values using the automatic lookup in class paramenters definitions:

```python
# ntp/manifests/init.pp
class ntp (
  Boolean $autoupdate,
  String  $service_name,
) {
 ...
}
```

Puppet will lookup the variables using the namespace that module has, in this case will try to solve usign the main hiera module file and search for ntp::autoupdate and ntp::service_name variables.
# eyaml: handling secrets in hiera

[INDEX](../../README.md)

## Overview:
Puppet plugin for Hiera to encrypt values using keys. Can encrypts plain text strings and entire files. 

## using eyaml in hiera and CLI:

1. Create the keys:

```bash
$ eyaml createkeys
$ mv keys/* /etc/puppetlabs/puppet/eyaml/

# Set permissions according your isnstallation
```

1. To use the command with this keys, a default config file is needed: 
   1. /etc/eyaml/config.yaml.
   2. ~/.yaml/config.yaml.
   3. EYAML_VAULT env variable.

```yaml
pkcs7_public_key: /etc/puppetlabs/puppet/eyaml/public_key.pkcs7.pem
pkcs7_private_key: /etc/puppetlabs/puppet/eyaml/private_key.pkcs7.pem
```

1. Create a hiera eyaml location:
   
```yaml
---
version: 5
defaults:  # Used for any hierarchy level that omits these keys.
  datadir: data         # This path is relative to hiera.yaml's directory. Ex: ./data dir location.
  data_hash: yaml_data  # Use the built-in YAML backend.

hierarchy:

  ... TRUNCATED DATA ...

  # Using eyaml for encrypted data
  - name: "Per-datacenter secret data (encrypted)"
    lookup_key: eyaml_lookup_key   # Uses non-default backend.
    path: "secrets/%{facts.whereami}.eyaml"
    options:
      pkcs7_private_key: /etc/puppetlabs/puppet/eyaml/private_key.pkcs7.pem
      pkcs7_public_key:  /etc/puppetlabs/puppet/eyaml/public_key.pkcs7.pem

  ... TRUNCATED DATA ...

  - name: "Common data"
    path: "common.yaml"
```

## Using eyaml CLI

```bash
# Encrypt string
$ eyaml encrypt -s secretPassw0rd

# Encrypt file
$ eyaml encrypt -f file.plaintext

# Decrypt a encypted string
$ eyaml encrypt -s "ENC[PKCS7,MIIBmQY.... TRUNCATED_DATA ...TCo=]"

# Decrypt file
$ eyaml decrypt -f file.encrypt
```

## Using eyaml in Hiera

```bash
# Using eyaml edit to see values and edit inline
$ eyaml edit file.encrypt

# Adding hiera data using edit
$ eyaml edit secrets/newyork.yaml
# the command will open a vi editor and using this type of structure (DEC::PKCS7[YOUR_STRING]!) we can encrypt a variable:
mysql::password: DEC::PKCS7[SuperS3cretP@assword]!
:x
```
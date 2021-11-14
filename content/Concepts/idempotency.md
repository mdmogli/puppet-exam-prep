# Idempotency

[INDEX](../../README.md)

## Overview
Puppet will ensure to mantain a desire state of the system, if the system comply with the manifest, puppet do nothing.

### Example

#### non-idempontent bash script
in the first run the script will install the package, in the second time the script will try to the same.
```bash
  #!/bin/bash
  $ apt install sysstat
```

#### idempontent puppet
in the first run the puppet will install the package, in the second puppet do nothing.
```bash
  package { 'sysstat':
    ensure => installed,
  }
```
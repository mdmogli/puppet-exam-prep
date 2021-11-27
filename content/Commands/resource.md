# puppet resource

[INDEX](../../README.md)

## Overview:
Uses the Puppet RAL to directly interact with the system, it converts current system state into Puppet code.

## Examples:

```bash
# Create puppet code from an existing user
$ puppet resource user luke
user { 'luke':
 home => '/home/luke',
 uid => '100',
 ensure => 'present',
 comment => 'Luke Kanies,,,',
 gid => '1000',
 shell => '/bin/bash',
 groups => ['sysadmin','audio','video','puppet']
}

# Create a user using puppet resource user
$ puppet resource user luke ensure=present
Notice: /User[luke]/ensure: created
user { 'luke':
    ensure => 'present',
}

# List all resources
$  puppet describe --list
```
# Namespaces & Autoloading

[INDEX](../../README.md)

## Overview
Class and defined type names can be broken up into segments called namespaces which enable the autoloader to find the class or defined type in your modules.

### Autoloader behavior

| Name                   | File path                                            |
| ---------------------- | ---------------------------------------------------- |
| apache                 | <MODULE DIRECTORY>/apache/manifests/init.pp          |
| apache::mod            | <MODULE DIRECTORY>/apache/manifests/mod.pp           |
| apache::mod::passenger | <MODULE DIRECTORY>/apache/manifests/mod/passenger.pp |

**Note**: The init.pp file always contains a class or defined type with the same name as the module.

# Resource Abstraction Layer

[INDEX](../../README.md)

## Overview
Puppet abstracts every resource using the RAL. We declare the WHAT, the RAL decides the HOW.

### How it works:

1. puppet code: high level descriptions of the desired state we have for our servers.
2. The RAL: Waht allows us to use "resources" to write our puppet code at a high level.
3. Providers: The part of the RAL that takes our high level coce and overt it so the managed system can use it.

| Resource Name	              | Providers                  |
| --------------------------- | -------------------------- |
| User                        | adduser                    |
|                             | useradd                    |
| Package                     | yum                        |
|                             | apt                        | 

## example: puppet decribe command
Checks the providers of the package resource:
```bash
  $ puppet describe package
```

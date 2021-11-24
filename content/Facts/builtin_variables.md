# Builtin Variables

[INDEX](../../README.md)

## Overview:
These variables are called trusted facts, server facts, agent facts, server variables, and compiler variables.

## Trusted facts:
Trusted facts are extracted from the node's certificate. You can access using $trusted['fact_name'].

## Server facts:
Facts that cannot be overwritten by client side facts.  You can access using $server_facts['fact_name'].

## Agent facts:
Puppet agent and Puppet apply both add several extra pieces of info to their facts before requesting or compiling a catalog. They are top-scope variables or elements in the $facts hash.

## Server Variables:
Several variables are set by the compiling Puppet server, useful when managing Puppet with Puppet. Server variables are not available in the $facts hash.

## Compiler variables:
Compiler variables are set in every local scope by the compiler during compilation, used when implementing complex defined types. Compiler variables are not available in the $facts hash.

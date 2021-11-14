# Relationship and Ordering

[INDEX](../../README.md)

## Overview
Resources are included and applied in the order they are defined in their manifest but only if the resource has no implicit relationship with another resource.

### Refreshing and notification
Some resource types can refresh when one of their dependencies changes. Built-in resource types that can refresh are service, exec, and package.

## Relationship 

### using metaparameters
* before: Applies a resource before the target resource.
* require: Applies a resource after the target resource.
* notify: Applies a resource before the target resource. Refresh on changes.
* subscribe: Applies a resource after the target resource. Refresh on changes.

### usign chaining arrows
* (->): The ordering arrow.
* (~>): The notifying arrow.

**Note**: Both chaining arrows have a reversed form (<- and <~).

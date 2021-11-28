# Defined types

[INDEX](../../README.md)

## Overview
Code that we can use repeatedly with different parameters within our module avoiding the multiple class declaration. Classes are singleton, you cannot redeclare a class multiple times. Definde types behave like resources.

## Create a new define type
```bash
    $ pdk new class defined_type NAME
```

## Example of a define type
As you can see, is very similar to a class but the definition word change to **define** instead of **class**. 

```python
define apache::vhost (
  Integer $port,
  ...
) {
    include apache

    resources ...
}
```

## Using a defined type:
```python
class myclass {
    include apache

    apache::vhost { 'puppet_project':
        port => 80,
        ...
    }

    apache::vhost { 'puppet_project_dev':
        port => 8081,
        ...
    }
}
```

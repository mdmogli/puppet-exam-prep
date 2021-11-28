# Hiera Lookup Layers

[INDEX](../../README.md)

## Layered hierarchies 
Hiera uses layers of data with a hiera.yaml for each layer. A lookup works as following:

- global → environment → module.

**Note**: Merge lookups do not transcend configuration levels (see unique, hash and deep merge behavior)

### 1- Global layer:
is located, by default, in: $confdir/hiera.yaml

### 2- Environment layer:
is located, by default, in ENVIRONMENT_DIR/hiera.yaml

### 3- Module layer:
is located, by default, in MODULE/hiera.yaml.

## Looking up data from hiera:

When looking up a key, Hiera searches up to four hierarchy layers of data, in the following order:

1. Global hierarchy.
1. The current environment's hierarchy.
1. The indicated module's hierarchy, if the key is of the form MODULE_NAME::SOMETHING.
1. If not found and the module's hierarchy has a default_hierarchy entry in its hiera.yaml — the lookup is repeated if steps 1-3 did not produce a value.
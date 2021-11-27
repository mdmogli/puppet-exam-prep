# puppet module

[INDEX](../../README.md)

## Overview:
This subcommand can find, install, and manage modules from the Puppet Forge, a repository of user-contributed Puppet code. It can also generate empty modules, and prepare locally developed modules for release on the Forge (deprecated, use pdk instead).


## Examples

```bash
# Show modified files of an installed module.
$ puppet module changes MODULENAME

# Install a module from the Puppet Forge or a release archive.
$ puppet module install MODULENAME

# List installed modules
$ puppet module list

# Uninstall a puppet module.
puppet module uninstall MODULENAME

# Upgrade a puppet module.
$ puppet module upgrade MODULENAME

```
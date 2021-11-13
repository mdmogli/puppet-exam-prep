# The PuppetFile

[INDEX](../../README.md)

## Overview
Specifies detailed information about each environment's Puppet code and data. Both Code Manager and r10k use a Puppetfile to install and manage the content of your environments.

### A Puppetfile controls content such as:
1. Modules from the Forge
1. Modules from Git repositories
1. Data from Git repositories

### Puppetfile Example:
```txt
forge 'http://forge.puppetlabs.com'

# To install puppet modules inside this directory
moduledir 'thirdparty'

# Module downloaded from forge with no version specified, takes latest
mod 'puppetlabs-ntp'

# Module downloaded from forge with version latest specified
mod 'puppetlabs-ntp', :latest

# Module downloaded from forge with version specified
mod 'puppetlabs-ntp', '9.1.0'

# Module from custom repo using ref (This can be used with a git commit, branch reference, or a tag):
mod 'puppetlabs-ntp',
  :git => 'git@github.com/puppetlabs-ntp.git',
  :ref => 'v2.8.0'

# Module from custom repo using tag:
mod 'puppetlabs-ntp',
  :git => 'git@github.com/puppetlabs-ntp.git',
  :tag => 'v2.8.0'

# Module from custom repo using commit:
mod 'puppetlabs-ntp',
  :git => 'git@github.com/puppetlabs-ntp.git',
  :commit  => '83401079053dca11d61945bd9beef9ecf7576cbf'

# Module from custom repo using branch:
mod 'puppetlabs-ntp',
  :git => 'git@github.com/puppetlabs-ntp.git',
  :branch => 'branch_name'

# Module from custom repo using branch variable:
mod 'puppetlabs-ntp',
  :git => 'git@github.com/puppetlabs-ntp.git',
  :branch => $branch_variable
  :default_branch => 'master'

# External data from custom repo and installing in an specific directory:
mod 'hiera-data',
  :git => 'git@github.com/hiera-data.git',
  :install_path  => 'externa_data'

```

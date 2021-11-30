# Metaparameters

[INDEX](../../README.md)

## Overview
Are attributes that work with any resource type.

### alias: 
Creates an alias for the resource

```python
file { '/etc/ssh/sshd_config': 
  owner => root,
  group => root,
  alias => 'sshdconfig',
 }

File['sshdconfig'] {
  mode => '0644',
}
```

### before: 
Causes the resource to be applied before the dependent resources. 

### notify:
This resource is applied before the notified resources. If Puppet makes changes to this resource, it causes all of the notified resources to refresh. Refresh behavior varies by resource type: for example, services restart and mounts unmount and re-mount. Not all types can refresh.

### require:
The required resources are applied before this resource.

```python
# Using an array of Packages resources
file { '/etc/ssh/sshd_config':
  ensure  => file,
  owner   => root,
  group   => root,
  require => Package['httpd', 'example1'],
}

# Using an Array of mix resources
file { '/etc/ssh/sshd_config':
  ensure  => file,
  owner   => root,
  group   => root,
  require => [ Package['httpd'], Service['crond'] ],
 }
```

### subscribe:
The subscribed resources are applied before this resource. If Puppet makes changes to any of the subscribed resources, it causes this resource to refresh.

### loglevel:
Sets the level at which information is logged. Values: emerg, alert, crit, err, warning, notice, info, verbose, debug.

### schedule:
Govern when Puppet is allowed to manage this resource. 

```python
schedule { 'everyday': 
  period => daily,
  range  => "2-4"
  }

exec { "/usr/bin/apt-get update": 
  schedule => 'everyday'
}
```

### noop:
"no-op" mode = dry-run

### tag:
Add tags to the associated resource.

```python
file {'/etc/hosts':
  ensure => file,
  source => 'puppet:///modules/site/hosts',
  mode   => '0644',
  tag    => ['bootstrap', 'minimumrun', 'mediumrun'],
}
```

```bash
    # useful for applying a subset of a host's configuration
    $ puppet agent --test --tags bootstrap
```

### stage
stages are an additional way to order resources. By default there is only one stage, named main and All resources are automatically associated to it unless you assigned to one another. This metaparameter can only be used on classes.

```python
stage { 'pre': 
  before => Stage['main'],
}

class { 'apt-updates': 
  stage => 'pre',
}
```

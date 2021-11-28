# Class parameters

[INDEX](../../README.md)

## Class parameters: hiera vs params.pp

### params.pp pattern (deprecated)
The params.pp pattern takes advantage of the Puppet class inheritance behavior. It is a class that do nothing but set variables for other classes (default values), The rest of the classes in the module inherit from the params class.

An example params class:
```python
# ntp/manifests/params.pp
class ntp::params {
  $autoupdate = false,
  $default_service_name = 'ntpd',

  case $facts['os']['family'] {
    'Debian': {
      $service_name = 'ntp'
    }
    'RedHat': {
      $service_name = $default_service_name
    }
  }
}
```

A class that inherits from the params class and uses it to set default parameter values:
```python
class ntp (
  $autoupdate   = $ntp::params::autoupdate,
  $service_name = $ntp::params::service_name,
) inherits ntp::params {
 ...
}
```

### hiera pattern
In this case, we use hiera to grab the values of the variables without using a class. Puppet can grab these values using the automatic lookup in class paramenters definitions:

```python
# ntp/manifests/init.pp
class ntp (
  Boolean $autoupdate,
  String  $service_name,
) {
 ...
}
```

Puppet will lookup the variables using the namespace that module has, in this case will try to solve usign the main hiera module file and search for ntp::autoupdate and ntp::service_name variables using the behavior Global (1) -> Environment (2) -> Module (3).
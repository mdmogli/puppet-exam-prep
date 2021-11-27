# Resource default statements

[INDEX](../../README.md)

## Overview
Enable you to set default attribute values for a given resource type.

### Example
```python
# Note that the exec resource has a capilal "E"
Exec {
  path        => '/usr/bin:/bin:/usr/sbin:/sbin',
  environment => 'RUBYLIB=/opt/puppetlabs/puppet/lib/ruby/site_ruby/2.1.0/',
  logoutput   => true,
  timeout     => 180,
}
```

### behavior
In this example, each "exec" resource that omits a given attribute uses that attribute’s default value, such as, path, environment, logoutput adn timeout.
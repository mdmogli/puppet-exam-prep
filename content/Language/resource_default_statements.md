# Resource default statements

[INDEX](../../README.md)

## Overview
Enable you to set default attribute values for a given resource type.

### Example
```python
Exec {
  path        => '/usr/bin:/bin:/usr/sbin:/sbin',
  environment => 'RUBYLIB=/opt/puppetlabs/puppet/lib/ruby/site_ruby/2.1.0/',
  logoutput   => true,
  timeout     => 180,
}
```

### behavior
Each resource type that omits a given attribute uses that attribute’s default value.
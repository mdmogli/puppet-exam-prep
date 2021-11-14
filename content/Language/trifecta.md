# The trifecta: package, file, and service

[INDEX](../../README.md)

## Overview
Package, file, service: Learn it, live it, love it. Even if this is the only Puppet you know, you can get a lot done.

### Example
```python
package { 'openssh-server':
  ensure => installed,
}

file { '/etc/ssh/sshd_config':
  source  => 'puppet:///modules/sshd/sshd_config',
  owner   => 'root',
  group   => 'root',
  mode    => '0640',
  notify  => Service['sshd'], # sshd restarts whenever you edit this file.
  require => Package['openssh-server'],
}

service { 'sshd':
  ensure     => running,
  enable     => true,
}
```

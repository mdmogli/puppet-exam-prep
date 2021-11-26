# PDK

[INDEX](../../README.md)

## Overview:
pdk (puppet development kit) is a tool to create modules, classes. A installation is needed in the system.

### Example

1. Create a new module skeleton:
```bash
# This command will ask some question, such as module name, operating system support, author, etc
$ pdk new module

# using deprecated command:
$ puppet module generate NAME
```

2. Create a new class:
```bash
# Running this command inside the root module folder
$ pdk new class class_name
pkd (INFO): Creating '/etc/puppetlabs/code/environment/production/modules/module_name/manifest/class_name.pp' from template.
pkd (INFO): Creating '/etc/puppetlabs/code/environment/production/modules/module_name/spec/classes/class_name_spec.rb' from template.

# The following command will create a file called init.pp, that is the main class directory for the module
$ pdk new class module_name
pkd (INFO): Creating '/etc/puppetlabs/code/environment/production/modules/module_name/manifest/init.pp' from template.
pkd (INFO): Creating '/etc/puppetlabs/code/environment/production/modules/module_name/spec/classes/init_spec.rb' from template.
```

3. Files in modules:
In order to use files in modules, is need to place those files in $MODULEDIR/files directory and using the puppet URL lookup, you will be able to use it in your classes:

```python
class ntp::config {

  file { 'ntp_config':
    ensure  => present,
    owner   => "root",
    group   => "root",
    mode    => "644",
    path    => "/etc/ntp.conf",
    source  => "puppet:///modules/ntp/ntp.conf",
  }
}

```

4. Templates in modules:
In order to use templates in modules, is need to place those files in $MODULEDIR/templates directory and using the puppet URL lookup, you will be able to use it in your classes:

```python
# Using epp
class ntp::config {

  file { 'ntp_config':
    ensure  => present,
    path    => "/etc/ntp.conf",
    owner   => "root",
    group   => "root",
    mode    => "644",
    content => epp('ntp/template_name.epp'),
  }
}

# Using erb
class ntp::config {

  file { 'ntp_config':
    ensure  => present,
    path    => "/etc/ntp.conf",
    owner   => "root",
    group   => "root",
    mode    => "644",
    content  => template('ntp/template_name.erb'),
  }
}


```
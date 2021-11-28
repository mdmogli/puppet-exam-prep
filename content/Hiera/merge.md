# Hiera Lookup Merge Behavior

[INDEX](../../README.md)

## Merge behaviors:
There are four merge behaviors to choose from: ***first, unique, hash, and deep***.

### First:
A first-found lookup doesn’t merge anything: it returns the first value found for the key, and ignores the rest. This is **Hiera’s default behavior**.

### Unique (used for **array** types only):
It walks trough each hierachy level, collects all instances of the key and returns an array of uniques values.

```yaml
# top level of hiera data (ex: nodes/%{trusted.certname}.yaml)
system::packages: ['php7', 'apache', 'java']

# bottom level of hiera data (ex: common.yaml)
system::packages: ['libc++', 'autoconf', 'java']

# will return (reapeted java package, only once):
['php7', 'apache', 'java', 'libc++', 'autoconf']
```

### Hash (used for **hash** types only):
It walks trough each hierachy level, expects all matching values to be hashes and merge all in one hash with first match only.

```yaml
# top level of hiera data (ex: nodes/%{trusted.certname}.yaml)
system::repos: 
  application:
    baseurl: http://yum.example.com/rhel8/apps
  test:
    baseurl: http://yum.example.com/rhel8/test_app

# bottom level of hiera data (ex: common.yaml)
system::repos: 
  dba:
    baseurl: http://yum.example.com/rhel8/dba
  test:
    baseurl: http://yum.example.com/rhel8/test
    enable: 0

# will return, notice that will not return the value of enable flag:
{
  "application" => { "baseurl" => "http://yum.example.com/rhel8/apps" },
  "test"        => { "baseurl" => "http://yum.example.com/rhel8/test_app" },
  "dba"         => { "baseurl" => "http://yum.example.com/rhel8/dba" },
}
```

### Deep (used for **hash** types only):
Similiar behavior than Hash but it combines all keys in one hash (check enable key in test repo). It walks trough each hierachy level, expects all matching values to be hashes and merge all in one hash.

```yaml
# top level of hiera data (ex: nodes/%{trusted.certname}.yaml)
system::repos: 
  application:
    baseurl: http://yum.example.com/rhel8/apps
  test:
    baseurl: http://yum.example.com/rhel8/test_app

# bottom level of hiera data (ex: common.yaml)
system::repos: 
  dba:
    baseurl: http://yum.example.com/rhel8/dba
  test:
    baseurl: http://yum.example.com/rhel8/test
    enable: 0

# will return:
{
  "application" => { "baseurl" => "http://yum.example.com/rhel8/apps" },
  "test"        => { 
    "baseurl" => "http://yum.example.com/rhel8/test_app",
    "enable"  => 0
  },
  "dba"         => { "baseurl" => "http://yum.example.com/rhel8/dba" },
}
```

## Lookup behavior from hiera configuration
You can set it up the lookup behavior in any file of your hierarchy. When we set this parameter for a variable, our lookup will use this method as default for a given variable. In this example we will put on our bottom level (common.yaml) for our system::repos variable:

```yaml
# top level of hiera data (ex: nodes/%{trusted.certname}.yaml)
system::repos: 
  application:
    baseurl: http://yum.example.com/rhel8/apps
  test:
    baseurl: http://yum.example.com/rhel8/test_app

# bottom level of hiera data (ex: common.yaml)
lookup_options:
  system::repos:
    merge: deep

system::repos: 
  dba:
    baseurl: http://yum.example.com/rhel8/dba
  test:
    baseurl: http://yum.example.com/rhel8/test
    enable: 0
```
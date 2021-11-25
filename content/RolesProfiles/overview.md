# Roles and profiles

[INDEX](../../README.md)

## Overview:
The roles and profiles method separates your code into three levels:

1. Component modules — Normal modules that manage one particular technology, for example puppetlabs/apache.
1. Profiles — Wrapper classes that use multiple component modules to configure a layered technology stack.
1. Roles — Wrapper classes that use multiple profiles to build a complete system configuration.

### Example

```javascript
class role::jenkins::master {
  include profile::base
  include profile::server
  include profile::jenkins::master
}           
```

## Rules for profile classes:
1. You can safely include any profile multiple times — don't use resource-like declarations on them.
2. Profiles can include other profiles.

## Rules for role classes:
1. Declare profile classes with include, Don't declare any component classes or normal resources in a role. Optionally, roles can use conditional logic to decide which profiles to use.
2. Roles should not have any class parameters of their own.
3. Roles should not set class parameters for any profiles.
4. name should be based on your business's conversational name, ex "Jenkins master" -> role::jenkins::master.

## Data lookups

This profile uses the automatic class parameter lookup to request data.
```javascript
# Example Hiera data
profile::jenkins::jenkins_port: 8000
profile::jenkins::java_dist: jre
profile::jenkins::java_version: '8'
 
# Example manifest
class profile::jenkins (
  Integer $jenkins_port,
  String  $java_dist,
  String  $java_version
) {
# ...
```

This profile omits the parameters and uses the lookup function:
```javascript
class profile::jenkins {
  $jenkins_port = lookup('profile::jenkins::jenkins_port', {value_type => String, default_value => '9091'})
  $java_dist    = lookup('profile::jenkins::java_dist',    {value_type => String, default_value => 'jdk'})
  $java_version = lookup('profile::jenkins::java_version', {value_type => String, default_value => 'latest'})
  # ...
```

## How to use it:
In your main main control repo manifest (control-repo/environment/manifests/site.pp) add the role to your nodes.

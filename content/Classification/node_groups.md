# Classification and environment node groups

[INDEX](../../README.md)

## Classification
Classification stands in what classes should puppet be applied to a node that request for a catalog. Puppet classifies nodes in two ways:

1. Using an External Node Classifier (ENC):
   1. Enterprise Console (default in puppet enterprise setup)
   2. Foreman (OpenSource Lifecycle management tool)
   3. Satellite (RedHat Lifecycle management tool)
2. Using the main manifest file: site.pp file, very useful when you use the profile/role approach. 

## ENC puppet enterprise console, two main types of node groups:

### Classification node groups:
Configure nodes by assigning classes, parameters, and variables to them. 

1. You can override variables from web console in the "Configuration" tab.
1. In the data section, you can override paramester from parent class definition.
1. In the variables tab, you can set up global variables.  

### Environments node groups:
Configure nodes by assigning environments (git branches) to them.

1. Must be a direct child of the All Environments node group
1. Must not include child groups, except any one-time run exception subgroups used for canary testing (puppet agent -t --environment env_name)
1. Must be specified as an environment group in the group metadata
1. Must not include classes or configuration data

## Using main manifest way:

```yaml
# /etc/puppetlabs/code/environments/production/manifests/site.pp

node "host1.example.com" {
    include role::webserver
}

node "host2.example.com" {
    include profile::webserver
    include profile::database
}

node /*.example.com/ {
    include class1
    include class2
}

node default {
    include class3
    include class4
}
```

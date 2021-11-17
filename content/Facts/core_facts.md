# Builtin Core facts

[INDEX](../../README.md)

## Overview:
Facts that ships with facter app. Not all of them apply to every system. You can access facts in your Puppet manifests as $fact_name or $facts[fact_name].

## Examples

```bash
$ facter os
{
  architecture => "x86_64",
  family => "RedHat",
  hardware => "x86_64",
  name => "RedHat",
  release => {
    full => "8.3",
    major => "8",
    minor => "3"
  },
  selinux => {
    config_mode => "permissive",
    config_policy => "targeted",
    current_mode => "permissive",
    enabled => true,
    enforced => false,
    policy_version => "32"
  }
}
$ facter os.family
RedHat
$ facter os.release.full
8.3
```

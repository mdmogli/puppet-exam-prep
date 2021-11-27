# Plans

[INDEX](../../README.md)

## Overview:
tie together multiple tasks, scripts, commands, and even other plans. plans can be writen in the Puppet language and yaml. And like tasks, plans are packaged in modules and can be shared on the Forge.

1. The full name of the plan, formatted as MODULE::PLAN.
1. Any plan parameters, as PARAMETER=VALUE.
1. (If required) The username and password to access the target. Pass these in as --user and --password command-line options.
1. PROJECT DIRECTORY/plans/

## Examples:

```bash
    # Run a plan from a module with parameters
    $ bolt plan run mymodule::myplan load_balancer=lb.myorg.com

    # Run a plan from a module with parameters with complex structure
    $ bolt plan run mymodule::myplan load_balancers='["lb1.myorg.com", "lb2.myorg.com"]'

    # passing structured data (array, hash, etc)
    $ bolt plan run mymodule::myplan --params '{"load_balancers": ["lb1.myorg.com", "lb2.myorg.com"]}'
```

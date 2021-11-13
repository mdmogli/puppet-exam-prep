# Tasks

[INDEX](../../README.md)

## Overview:
Bolt can run Puppet tasks on remote targets without requiring any Puppet infrastructure. 

In order for Bolt to find a task, the task must be in a module on the modulepath or in the tasks/ directory in your Bolt project

1. The full name of the task, formatted as <MODULE::TASK>, or as <MODULE> for a module's main task (the init task).
1. Any task parameters, as parameter=value.
1. The targets on which to run the task and the connection protocol, with the targets command-line option.

## Examples:

```bash
    # Run a mysql task target nodes
    $ bolt task run mysql::sql database=mydatabase --targets neptune sql="SHOW TABLES"

    # run status actions of package module
    $ bolt task run package --targets servers action=status name=vim 

    # passing structured data (array, hash, etc)
    $ bolt task run mymodule::mytask --targets app1.myorg.com load_balancers='["lb1.myorg.com", "lb2.myorg.com"]'

    # passing multiple structure data, same from a file
    $ bolt task run mymodule::mytask --targets app1.myorg.com --params '{"load_balancers": ["lb1.myorg.com", "lb2.myorg.com"]}'
    $ bolt task run mymodule::mytask --targets app1.myorg.com --params @param_file.json

    # run with sudo, will prompt for sudo password
    $ bolt task run apache::ctl command=restart --run-as root --sudo-password --nodes servers
```
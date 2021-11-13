# Bolt

[INDEX](../../README.md)

## Overview:
opensource orchestation tool that allows us to run ad-hoc commands, tasks and plans. Bolt use SSH as a default transport mech. In order to run bolt without user/pass, ssh pubkey is needed, bolt will use the key stored in ~/.ssh/.

Main configuration file: ~/puppetlabs/bolt/bolt.yaml

```yaml
    modulepath: "MODULEPATH"
    inventoryfile: "INVFILE"
    concurrency: 10
    ssh:
        user: USER
```
## Examples:

```bash
    # Run command CMD on target nodes
    $ bolt command run 'CMD' --nodes|--target node1,node2

    # Run local script on targets
    $ bolt command run ./script.sh --nodes|--target node1,node2
    $ bolt script run ./script.sh --targets servers arg1 arg2  # with arguments

    # Run script without uploading the script
    $ bolt command run @script.sh --targets servers
    $ cat script.sh | bolt command run - --targets servers   # from stdin

    # Runing from an specific inventory file
    $ bolt command run 'pwd' -i inventory.yaml --targets servers,databases
    $ bolt command run 'pwd' -i inventory.yaml --targets 'databases*'

    # Read targets from file and stdin
    $ bolt command run 'pwd' --targets '@targets.txt'
    $ cat targets.txt | bolt command run 'pwd' --targets -

    # Copy files
    $ bolt file upload local_file remote_file --nodes|--target node1,node2
    $ bolt file download /path/to/source /path/to/destination --targets servers

    # specify credentials (ssh user/pass)
    $ bolt command run 'pwd' --targets servers --user bolt --password puppet
    $ bolt command run 'pwd' --targets servers --user bolt --password-prompt # prompt for pass

    # specify transport, ex to run on win target node
    $ bolt command run 'Get-Location' --targets windows.example.org --transport winrm

    # steam the output: see what is happening on a target as an action runs
    $ bolt command run 'yum update -y' --targets servers --stream

    # apply puppet code
    $ bolt apply manifests/servers.pp --targets servers

    # run tasks, with parametes (parameter=value)
    $ bolt task run facts --targets servers
    $ bolt task run package action=status name=apache2 --targets servers

    # run a plan, with parametes (parameter=value)
    $ bolt plan run myplan
    $ bolt plan run reboot targets=servers

```
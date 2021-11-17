# PQL

[INDEX](../../README.md)

## Overview:
Queries are performed by issuing an HTTP GET or POST request, specifying a query URL parameter (in the GET case) or a JSON-valued payload in the POST case.

## Basic Breakdown

```bash
$ puppet query '<entity> [<projection>] { <filters> <modifiers> }'
```

## Examples
1. Using CLI and REST API with curl
```bash
    # CLI query without/with SSL
    $ puppet query '<PQL query>' --urls http://puppetdb:8080
    $ puppet query '<PQL query>' --urls https://puppetdb:8081

    # Curl query using GET/POST without SSL
    $ curl -X GET http://puppetdb:8080/pdb/query/v4 --data-urlencode 'query=<PQL query>'
    $ curl -X POST http://puppetdb:8080/pdb/query/v4 -H 'Content-Type:application/json' -d '{"query":"<PQL query>"}'
```

1. Running a query in puppet code:
```python
    # using in the code
    $debian_nodes_query = 'nodes[certname]{facts{name = "operatingsystem" and value = "Debian"}}'
    $debian_nodes = puppetdb_query($debian_nodes_query).map |$value| { $value["certname"] }
    notify {"Debian nodes":
        message => "Your debian nodes are ${join($debian_nodes, ', ')}",
    }
```

1. Entities:
```bash

    # Resource entity
    $ puppet query "resources[certname, type, title, parameters] { exported = true }"

    # Nodes entity
    $ puppet query "nodes[certname] { certname ~ '^web' }"

    # Facts entity
    $ puppet query "facts[name] { group by name }"

    # Reports entity
    $ puppet query "reports { certname = 'node1.com' }"

    # Inventory entity
    $ puppet query "inventory { facts.os.name = 'Ubuntu' }"
    $ puppet query "inventory { facts.os.name = 'Ubuntu' or facts.os.name = 'RedHat' }"

    # Mixin entities
    $ puppet query "inventory { facts.os.name = 'Ubuntu' and resources { type = 'Service' and title = 'apache' } }"
    $ puppet query "inventory { facts.os.name = 'Ubuntu' or facts.os.name = 'RedHat' and resources { type = 'Service' and title = 'apache' or title = 'httpd' } and environment = 'staging' }"
```




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
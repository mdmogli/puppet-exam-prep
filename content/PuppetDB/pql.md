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

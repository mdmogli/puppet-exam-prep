# PuppetDB Overview

[INDEX](../../README.md)

## Overview:
Collects data generated by puppet and saves in a PostgreSQL database and has the following featerure 

- Allow the use of exported resources.
- Opensource
- Provides an API to check data from the database.
- Provides CLI commands to query and export/import the main database.
- Has the PQL language to make queries.

## path config files:

- /etc/puppetlabs/puppetdb/conf.d
- /etc/puppetlabs/puppetdb/conf.d/config.ini  (main file)

| OS and Package	          | File                       |
| --------------------------- | -------------------------- |
| Red Hat-like (open source)  | /etc/sysconfig/puppetdb    |
| Red Hat-like (PE)	          | /etc/sysconfig/pe-puppetdb |
| Debian/Ubuntu (open source) | /etc/default/puppetdb      |
| Debian/Ubuntu (PE)          | /etc/default/pe-puppetdb   | 

## Useful CLI:

```bash
    # information about the status of the node
    $ puppet node status nodename

    # query the puppetDB database using PQL
    $ puppet query "nodes[certname] { catalog_environment = 'staging' }"

    # export database
    $ puppet db export database.tgz --anon "full|moderate|low"

    # import database
    $ puppet db import database.tgz

    # check metrics of puppet db using a SSH tunnel
    # 1- from your PC
    $ ssh -L 8080:localhost:8080 puppetdb_server
    # 2- from your browser, access to the following URL:
    http://localhost:8080
```
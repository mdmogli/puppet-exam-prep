# PE installation

[INDEX](../../README.md)

We have 3 types of installation:

## Text-mode installation
1. Download file from puppet.com:
   - https://puppet.com/try-puppet/puppet-enterprise/download/
1. Untar file downloaded and access to extracted folder.
1. run puppet installer:
    ```bash
        $ ./puppet-enterprise-installer
    ```
1. Select "text-mode" installer.
1. The only value needed to filled is the "console_admin_password".
1. In case of a split installation, we can select the following parameters in the installation procedure:
   1. "puppet_enterprise::puppet_master_host": puppet master
   1. "puppet_enterprise::console_host": Web console host.
   1. "puppet_enterprise::puppetdb_host": puppetDB service host.
   1. "puppet_enterprise::database_host": puppet postgresql service host.

## Text-mode installation using a pe.conf file.

1. run puppet installer:
    ```bash
        $ ./puppet-enterprise-installer -c /path/pe.conf
    ```

## Graphical-mode installation.

1. run puppet installer:
    ```bash
        $ ./puppet-enterprise-installer
    ```
1. Select graphical installation mode.
1. Access via web to the following link:
   - https://puppet-master-node:3000
1. Follows the steps via graphical mode.
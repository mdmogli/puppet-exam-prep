# Backups and restore

[INDEX](../../README.md)

## Backup

1. Backups infrastructure:
   ```bash
   $ puppet-backup create
   ```
   -  /var/puppetlabs/backups (default backups directory)

   You can specify these optional parameters:
   * --name=$BACKUP_NAME – Specifies a name for the backup file. Default: pe_backup-$TIMESTAMP.tgz.
   * --pe-environment=$ENVIRONMENT – Specifies an environment to back up. To ensure configuration is recovered correctly, this must be the environment where your primary server is located. Default: production.
   * --scope=$SCOPE_LIST – Specifies the data to back up: certs, code, config, puppetdb. Default: all.
   * --gpgkey=$KEY_ID – Specifies a GPG key ID to use for encrypting the backup file.
   * --force – Bypasses validation checks and ignore warnings.
1. Backup secret key:
   * /etc/puppetlabs/orchestration-services/conf.d/secrets/keys.json

## Restore

1. If you restore backup in a existing installation, purge the instance first:
   ```bash
   $ /opt/puppetlabs/bin/puppet-enterprise-uninstaller -p -d
   ```
1. Download and install PE infra: see PE installation.
1. Retore using the backups file:
   ```bash
   $ puppet-backup restore <BACKUP-FILENAME>
   ```
   You can specify these optional parameters:
   * --pe-environment=$ENVIRONMENT – Specifies an environment to restore. Default: production
   * --scope=$SCOPE_LIST – Specifies the data to restore: certs, code, config, puppetdb. Default: all
   * --force – Bypasses validation checks and ignore warnings.
1. Restore secret key:
   ```bash
   $ cp keys.json /etc/puppetlabs/orchestration-services/conf.d/secrets/
   ```
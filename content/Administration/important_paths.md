# Important paths

[INDEX](../../README.md)

### Main installation directory
1. Unix: /opt/puppetlabs
1. Win: Program Files at Puppet Labs\Puppet

### Executable binaries and symlinks
1. Binaries: /opt/puppetlabs/bin and /opt/puppetlabs/sbin
1. symlinks: /usr/local/bin

### modules and plugnis:
1. default installation modules: /opt/puppetlabs/puppet/modules
1. non-default: /etc/puppetlabs/code/environments/environment_name/modules

### Configuration files:
1. Unix: /etc/puppetlabs/puppet
1. Win: <COMMON_APPDATA>\PuppetLabs | C:\ProgramData\PuppetLabs\puppet\etc

## Logs:

### Main PE logs:
- /var/log/puppetlabs/

### puppet server logs
- /var/log/puppetlabs/puppetserver/

### puppet console logs
- /var/log/puppetlabs/console-services/

### Installer logs:
- /var/log/puppetlabs/installer/

### Database logs:
- /var/log/puppetlabs/postgresql/

### Orchestation logs:
-  /var/log/puppetlabs/orchestration-services/

### Agent logs
- /var/log/messages (redhat)
- /var/log/syslog (debian based)
- /var/adm/messages (solaris)
- event logs (Windows)

### Certificates:
- /etc/puppetlabs/puppet/ssl/certs

### Secret keys (to encrypt/decrypt inventory sensitive data):
- /etc/puppetlabs/orchestration-services/conf.d/secrets/keys.json
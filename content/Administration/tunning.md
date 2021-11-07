# Tunning Infra nodes

[INDEX](../../README.md)

### Tunning command:

-  Outputs optimized settings for PE services, it queries PuppetDB and outputs settings in YAML.

```bash
    $ puppet infrastructure tune
```

### Tunning parameters:

You must use the console (classification), add the parameter to the appropriate infrastructure node group using the method suitable for the parameter type:

Some examples are:

- puppet_enterprise::profile parameters including java_args, shared_buffers, and work_mem
- puppet_enterprise::puppetserver_ram_per_jruby
- puppet_enterprise::master::puppetserver::jruby_max_active_instances
- puppet_enterprise::master::puppetserver::jruby_max_requests_per_instance
 


### Executable binaries and symlinks
1. Binaries: /opt/puppetlabs/bin and /opt/puppetlabs/sbin
1. symlinks: /usr/local/bin

### modules and plugnis:
1. default installation modules: /opt/puppetlabs/puppet/modules
1. non-default: /etc/puppetlabs/code/environments/<environment>/modules

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
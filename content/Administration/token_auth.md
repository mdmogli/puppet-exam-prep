# Client tools Token based auth

[INDEX](../../README.md)

## Overview:

-  Authentication tokens allow a user to enter their credentials once, then receive an alphanumeric "token" to use to access different services or parts of the system infrastructure.
-  The puppet-access command allows users to generate and manage authentication tokens from the command line of any workstation.

### Global config file
- Unix: /etc/puppetlabs/client-tools/puppet-access.conf
- Win: C:/ProgramData/PuppetLabs/client-tools/puppet-access.conf

### user specific:
- ~/.puppetlabs/client-tools/puppet-access.conf

Config:
```json
    {
        "service-url": "https://<CONSOLE HOSTNAME>:4433/rbac-api",
        "token-file": "~/.puppetlabs/token",
        "certificate-file": "/etc/puppetlabs/puppet/ssl/certs/ca.pem"
    }
```

### Create a token:

```bash
$ puppet-access login
```

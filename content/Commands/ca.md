# puppetserver ca

[INDEX](../../README.md)

## Overview:
CLI command to manage the CA service

## Examples

```bash
# To sign a pending certificate request:
$ puppetserver ca sign --certname foo.example.com

# To list certificates and CSRs:
$ puppetserver ca list --all

# To revoke a signed certificate:
$ puppetserver ca revoke --certname foo.example.com

# To revoke the cert and clean up all SSL files for a given certname:
$ puppetserver ca clean --certname foo.example.com

# To create a new keypair and certificate for a certname:
$ puppetserver ca generate --certname foo.example.com

# To remove duplicated entries from Puppet's CRL:
$ puppetserver ca prune

# To enable verbose mode:
$ puppetserver ca --verbose <action>

# For more details, see the help output:
$ puppetserver ca --help
```
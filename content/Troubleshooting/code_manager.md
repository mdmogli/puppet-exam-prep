# Troubleshooting code manager

## Overview
Code Manager requires coordination between multiple components, including r10k and the file sync service.

### Check code manager logs
Code Manager logs to the Puppet Server log. By default, this log is in /var/log/puppetlabs/puppetserver/puppetserver.log

### Check code manager status
The command puppet-code status verifies that Code Manager and file sync are responding.

### Test the connection to the control repository:

To make sure that Code Manager can connect to the control repo, run:

```bash
$ puppet-code deploy --dry-run
```

### check syntax of puppet file:

```bash
$ r10k puppetfile check
Syntax OK
```

### Check sources of a Puppetfile
copy your puppet file to a custom dir (/tmp/test_puppetfile) and run:

```bash
$ sudo -H -u pe-puppet bash -c 'r10k puppetfile install'
Syntax 

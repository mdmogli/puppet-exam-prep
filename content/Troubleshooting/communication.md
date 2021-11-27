# Troubleshooting connections between components

## Overview
If agent nodes can't retrieve configurations, check for communication, certificate, DNS , and NTP issues.

### Agents can't reach the primary server
1. Verify that the primary server is reachable at a DNS name your agents recognize.
1. Verify that the pe-puppetserver service is running.

```bash
# from agent, test if puppet is reacheble
$ telnet PRIMARY_HOSTNAME 8140
```

### Agents don't have signed certificates
Agent certificates must be signed by the primary server.

```bash
# print server cert list
$ puppet cert list

# sign certificate
$ puppetserver ca sign NODENAME
```

### Agents aren't using the primary server's valid DNS name
1. To edit the primary server's hostname on nodes, in /etc/puppetlabs/puppet/puppet.conf, change the server setting to a valid DNS name.
2. To reset the primary server's valid DNS names, run:
   
```bash
$ /etc/init.d/pe-nginx stop
$ puppet cert clean PRIMARY_CERTNAME
$ puppet cert generate PRIMARY_CERTNAME --dns_alt_names=COMMA-SEPARATED_LIST_OF_DNS_NAMES
$ /etc/init.d/pe-nginx start
```

### Time is out of sync
The date and time must be in sync on the primary server's and agent nodes.

### Node certificates have invalid dates
The date and time must be in sync when certificates are created.

### A node is re-using a certname
If a node re-uses an old node's certname and the primary server retains the previous node's certificate. Clean the certificate, rerrun puppet on agent and sign the new one.
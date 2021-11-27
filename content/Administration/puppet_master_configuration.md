# Puppet Master configuration

[INDEX](../../README.md)

## Important Configuration path
1. Main directory: /etc/puppetlabs
1. Puppet components config directory: /etc/puppetlabs/COMPONENT/conf.d
   1. /etc/puppetlabs/console-services/conf.d   -> web console setups
   1. /etc/puppetlabs/puppetdb/conf.d           -> puppetdb service setups
   1. etc 
1. Puppet config directory: /etc/puppetlabs/puppet/
1. Puppet main config file: /etc/puppetlabs/puppet/puppet.conf

## PE core configuration:
```bash
[main]
server = server_name.domain     -> puppet server   
certname = agent_name.domain    -> agent server name
dns_alt_names = aliases         -> server aliases
user = pe-puppet                -> user which puppet runs
group = pe-puppet               -> user which puppet runs
environment_timeout = 0         -> how log puppet caches env info
module_groups = base+pe_only    -> selects puppet forge modules
environmentpath = path          -> location of the directory environment
basemodulepath = path           -> location puppet code and modules

[agent]
... Same values that agent main config

[master]
node_terminus = classifier      -> which node terminus is used when a puppet run.
storeconfigs = boolean          -> enable node data caching on server
storeconfigs_backend = puppetdb -> sets where the data will be store.
reports = puppetdb              -> sets which reports handler puppet uses.
always_retry_plugins = boolean  -> is set to false, will no try to reload resources types o features that failed.
disable_l18n = boolean          -> disable tranlsation messages.
catalog_terminus                -> enable an additional static compiler
ca = boolean                    -> set if master is working as the CA.
ca_ttl = 5y                     -> time where puppet agent cert is valid
autosign = path                 -> sets if the master will autosign based on rules (*.domain.com)
```
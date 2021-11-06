# Puppet agent configuration

## Important Configuration path
1. Main directory: /etc/puppetlabs
1. Puppet config directory: /etc/puppetlabs/puppet/conf.d/
1. Puppet main config file: /etc/puppetlabs/puppet/puppet.conf

## Puppet core configuration:
```bash
[main]
server = server_name.domain     -> puppet server   
certname = agent_name.domain    -> agent server name

# Optional core values
environment = env               -> defines the envirment where the agent get the code
sourceaddress = ip-address      -> defines which ip address the agent use to communcate with the puppet server
runinterval = 10m               -> puppet agent runs frequency (30m default)
waitforcert = boolean           -> whether or not the agent will attempt to reconnect if no response from master
noop = boolean                  -> no made changes
priority = integer nice value   -> niceness of the puppet process
report = boolean                -> agent will report to master or not
tags = strings                  -> tags that tag the server.
usecacheonfailure = boolean     -> if set to true, the agent will used the last successful catalog
ignoreschedules = boolean       -> ignore schedules within puppet code
prerun_command = command        -> run command before puppet runs
postrun_command = command       -> run command after puppet runs

# Debuging
trace = boolean                 -> print stack traces
profile = boolean               -> performance profiling
graph = boolean                 -> created .dot graph files
show_diff = boolean             -> saves a diff of any files changes during the run
```
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

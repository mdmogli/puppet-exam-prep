# Exported resources

[INDEX](../../README.md)

## Overview
Enable the Puppet compiler to share information among nodes.

### Example
```python
class myclassA {

    # exported resource
    @@host { "${hostname}":
        host_aliases    => "$fqdn",
        ip              => "$ipaddress",
    }
}

class myclassB {
   Host <<||>>
}
```

### Expected result:
all nodes that use myclassA will export information about /etc/hosts with they own ip and alias data. When a node include myclassB will create entries with his own data and also with the exported data, basically the /etc/hosts file will be populated with alias and ip of every node that use it.

# External facts

[INDEX](../../README.md)

## Overview:
Provide a way to use arbitrary executables, scripts or set facts statically with structured data. 

Location of these scripts:
1. /opt/puppetlabs/facter/facts.d/
2. /etc/puppetlabs/facter/facts.d/
3. /etc/facter/facts.d/
4. <MODULEPATH>/<MODULE>/facts.d/

## Examples:

### Executable facts:

```python
#!/usr/bin/env python
data = {"key1" : "value1", "key2" : "value2" }

for k in data:
    print "%s=%s" % (k,data[k])

```
```bash
$ chmod +x /etc/facter/facts.d/my_fact_script.py
or
$ chmod +x /etc/puppetlabs/facter/facts.d/my_fact_script.py
```

### Structured data facts:

```yaml
---
key1: val1
key2: val2
key3: val3
```
```json
{ "key1": "val1", "key2": "val2", "key3": "val3" }
```
```txt
key1=value1
key2=value2
key3=value3 
```

## Composing data:

```txt
my_org.my_group.my_fact1 = fact1_value
my_org.my_group.my_fact2 = fact2_value
```
```json
{
  "datacenter":
  {
    "location": "bfs",
    "workload": "Web Development Pipeline",
    "contact": "Blackbird"
  },
  "provision":
  {
    "birth": "2017-01-01 14:23:34",
    "user": "alex"
  }
}
```

## Troubleshooting:

```bash
$ puppet facts --debug

...
Debug: Facter: resolving facts from executable file "/tmp/test.sh".
Debug: Facter: executing command: /tmp/test.sh
Debug: Facter: key1-value1
Debug: Facter: ignoring line in output: key1-value1
Debug: Facter: process exited with status code 0.
Debug: Facter: completed resolving facts from executable file "/tmp/test.sh".
...
```

## Drawbacks

1. An external fact cannot internally reference another fact.
2. External executable facts are forked instead of executed within the same process.

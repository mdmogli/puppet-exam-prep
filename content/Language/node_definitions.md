# Node Definitions

[INDEX](../../README.md)

## Overview
Define what roles or classes to be applied to nodes. Put node definitions in the main manifest, which can be a single site.pp file, or a directory containing many files.

### examples:
```python
# <ENVIRONMENTS DIRECTORY>/<ENVIRONMENT>/manifests/site.pp
node 'www1.example.com' {
  include common
  include apache
  include squid
}
node 'db1.example.com' {
  include common
  include mysql
}

node 'www1.example.com', 'www2.example.com', 'www3.example.com' {
  include common
  include apache, squid
}

node /^www\d+$/ {
  include common
}

node /^(one|two)\.example\.com$/ {
  include common
}
```

### Node matching:

1. www01.example.com
2. A regex that matches www01.example.com
3. www01.example
4. A regex that matches www01.example
5. www01
6. A regex that matches www01
7. default

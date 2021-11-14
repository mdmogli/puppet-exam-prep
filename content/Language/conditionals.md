# Conditionals statements

[INDEX](../../README.md)

## Conditionals
1. if statement
2. unless statement
3. case statement
4. selector expression

### if statement
```python
    if $facts['is_virtual'] {
        warning('Tried to include class ntp on virtual machine; this node might be misclassified.')
    } elsif $facts['os']['family'] == 'Darwin' {
        warning('This NTP module does not yet work on our Mac laptops.')
    } else {
        include ntp
    }
```

### unless statement
```python
    unless $facts['memory']['system']['totalbytes'] > 1073741824 {
        $maxclient = 500
    }
```

### case statement
```python
    case $facts['os']['name'] {
        'RedHat', 'CentOS':  {
            include role::redhat
        }
        /^(Debian|Ubuntu)$/:  {
            include role::debian  
        }
        default:  {
            include role::generic 
        }
    }
```

### variable selector
```python
    $rootgroup = $facts['os']['family'] ? {
        'RedHat'           => 'wheel',
        /(Debian|Ubuntu)/  => 'wheel',
        default            => 'root',
    }
```
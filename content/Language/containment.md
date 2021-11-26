# Containment

[INDEX](../../README.md)

## Overview
1. include
2. require
3. contain

## include
Use include when you don't need to enforce anything in your current class. Sets no ordering. Use include as default option. Nowadays puppet runs in the order that you define the includes and resources within the class.

```python
    class myapp {
        include install_ntp
        
        package { 'myapp':
            ensure => present,
        } 
    }
```

## require
When resources from another class should be enforced before use require, sets ordering.

### example
```python
    class myapp {
    # Using the contain function ensures that relationships on myapp also apply to these classes
        require package_installer
        
        package { 'myapp':
            ensure => present,
        } 
    }
```

## contain
Similar behavior that include but a relationship is needed to run using the Class declaration. See example.

### example
```python
    class myapp {
    # Using the contain function ensures that relationships on myapp also apply to these classes
        contain myapp::install
        contain myapp::config
        contain myapp::service
        
        Class['myapp::install'] -> Class['myapp::config'] ~> Class['myapp::service']
    }
```

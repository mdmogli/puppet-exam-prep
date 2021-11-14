# Variables

[INDEX](../../README.md)

## Overview
Variables store values, after you've assigned a variable a value, you cannot reassign it.

### Abstract data types
```python
# Assignment
$content = "some content\n"

# multiple var assignment
[$a, $b, $c] = [1,2,3]      # $a = 1, $b = 2, $c = 3

#  You cannot change the value of a variable, but you can assign a different value to the same variable name in a new scope
$myvar = "Top scope value"
node 'www1.example.com' {
  $myvar = "Node scope value"
  notice( "from www1: $myvar" )
  include myclass
}

# puppet resolves the variable $homedir inside a string
$rule = "Allow * from $ipaddress"
file { "${homedir}/.vim":
  ensure => directory,
  ...
}
```

# Custom overview

[INDEX](../../README.md)

## Overview:
Puppet includes many built-in functions, such as md5, each, downcase, etc. They run on server side and the purpose is to returns a value or extend functionality (earch function case). 

Can be writen using:
- The Puppet language: better if you don't have ruby laguange skills.
- The Ruby functions API: more powerful.

Use cases:
- Evaluate templates.
- Do mathematical calculations.
- Look up values from an external source.
- Cause side effects that modify the catalog.
- Evaluate a provided block of Puppet code.

## Code style:

1. Prefix way:

function_name(argument, argument, ...) |$parameter, $parameter, ...| { code block }

```bash
$binaries = [
  "facter",
  "hiera",
  "mco",
]

# function call with lambda; runs block of code several times
each($binaries) |$binary| {
  file {"/usr/bin/$binary":
    ensure => link,
    target => "/opt/puppetlabs/bin/$binary",
  }
}
```

1. Chained way:

argument.function_name(argument, ...) |$parameter, $parameter, ...| { code block }

```bash
$binaries = [
  "facter",
  "hiera",
  "mco",
]

# function call with lambda; runs block of code several times
$binaries.each |$binary| {
  file {"/usr/bin/$binary":
    ensure => link,
    target => "/opt/puppetlabs/bin/$binary",
  }
}
```

## Module layout:

```
.
└───files
└───functions
│   │   function1.pp    # Using puppet language
│   │   function2.pp    # Using puppet language
└───lib
│   └───puppet
|       └───functions
│           │   function3.rb    # Using ruby API
│           │   function4.rb    # Using ruby API
│           │   ...
└───manifests
└───templates
...
```

## Example

1. Using puppet language:

```python
file: "<modulepath>/<modulename>/functions/sayhello.pp"

function mymodule::sayhello(String $myname) >> String {
    $greeting = "Hello ${myname}, how do you do?"
    $greeting
}

...

Class UseMyfunction {

    $greetings = mymodule::sayhello('Max')

    notify { "Output: ${greetings}" }

}
```

2. Using ruby API:
   
```python
file: <modulepath>/<modulename>/lib/puppet/functions/sayhello.rb

Puppet::Functions.create_function(:"mymodule::sayhello") do
    def sayhello(myname)
        return "Hello #{myname}, how do you do?"
    end
end

...

Class UseMyfunction {

    $greetings = mymodule::sayhello('Max')

    notify { "Output: ${greetings}" }

}
```
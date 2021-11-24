# Custom facts

[INDEX](../../README.md)

## Overview:
You can add custom facts by writing snippets of Ruby code on the primary Puppet server.

Loading custom facts:
1. $LOAD\_PATH, or the Ruby library load path.
2. The --custom-dir command line option.
3. The environment variable FACTERLIB.

### $LOAD\_PATH way:

Facter searches all directories in the Ruby $LOAD_PATH variable for subdirectories named Facter, and loads all Ruby files in those directories.

```
#~/lib/ruby
└── facter
    ├── rackspace.rb
    ├── system_load.rb
    └── users.rb
```

### the --custom-dir way
able to multiple --custom-dir options on the command line.

```bash
$ facter --custom-dir=./my_facts --custom-dir=./my_other_facts system_load users
```

### FACTERLIB environment variable way:
Facter also checks the environment variable FACTERLIB for a delimited set of directories.

```bash
$ export FACTERLIB="./my_facts:./my_other_facts"
$ facter system_load users
system_load => 0.25
users => thomas,pat
```

## Writing custom facts:

```ruby
# hardware_platform.rb
Facter.add('hardware_platform') do
  setcode do
    Facter::Core::Execution.execute('/bin/uname --hardware-platform')
  end
end

# osfamily.rb
Facter.add(:osfamily) do
  setcode do
    distid = Facter.value(:lsbdistid)
    case distid
    when /RedHatEnterprise|CentOS|Fedora/
      'redhat'
    when 'ubuntu'
      'debian'
    else
      distid
    end
  end
end
```

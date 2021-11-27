# rspec

[INDEX](../../README.md)

## Overview:
puppet module unit testing.

## Importan path
1. $MODULE/spec: base test module folder
2. $MODULE/spec/{classes, defines, tasks, functions, hosts}

### Examples

- An example of a unit test that checks the logrotate class
```python
# $MODULE/spec/classes/logrotate_rspec.rb
require 'spec_helper'

describe 'logrotate' do
  let(:title) { 'nginx' }

  it { is_expected.to contain_class('logrotate::setup') }

  it do
    is_expected.to contain_file('/etc/logrotate.d/nginx').with({
      'ensure' => 'present',
      'owner'  => 'root',
      'group'  => 'root',
      'mode'   => '0444',
    })
  end
end
```

### To test this unit test within your module, run:

```bash
$ sudo pdk test unit --tests=classes/logrotate_spec.rb
```

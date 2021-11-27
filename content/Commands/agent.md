# puppet agent

[INDEX](../../README.md)

## Overview:
Triger a one off puppet run using **puppet agent -t**.

## Examples

```bash
# run once an exit
$ puppet agent -o

# run in foreground
$ puppet agent -n

# verbose mode
$ puppet agent -v

# run -onv
$ puppet agent -t

# Compare current system with catalog but no apply changes
$ puppet agent -t --noop
```
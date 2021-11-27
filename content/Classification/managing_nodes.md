# Managing Nodes

[INDEX](../../README.md)

### View peding node request:
```bash
$ sudo puppetserver ca list
```

### To sign a pending request:
```bash
$ sudo puppetserver ca sign --certname <NAME>
```

## Remove agent nodes & recover a license (purge):
1. On agents: service puppet stop
1. On MoM: puppet node purge CERTNAME
1. if you have compilers: puppet agent -t

## Clean cert but mantain the licence:
1. On agents: service puppet stop
2. On MoM: puppetserver ca clean --certname CERTNAME
3. if you have compilers: puppet agent -t
   
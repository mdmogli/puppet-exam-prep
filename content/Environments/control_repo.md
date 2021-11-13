# Environments with Control Repo

[INDEX](../../README.md)

## Overview
To manage your Puppet code and data with either Code Manager or r10k, Git version control repository is needed. Git branches acts as a environments on puppet.

- Environments are created in /etc/puppetlabs/code/environments on the primary server.
- Default branch named production
- A Puppetfile to manage your environment content
- An environment.conf file that modifies the $modulepath setting to allow environment-specific modules and settings.

### Create a control repo:

1. Create a keypar to be used to syncronize with your GIT repo:
    ```bash
    $ ssh-keygen -t rsa -b 2048 -P '' -f /etc/puppetlabs/puppetserver/ssh/id-control_repo.rsa
    $ puppet infrastructure configure    # Set permissions to pe-puppet user
    ```
1. Create a new git repo using a template control-repo on github/gitlab/etc.
1. add the pub key to the repo and read/write permissions.
2. push your code to this remote repo.
3. on the primary issue the command below:
    ```bash
    $ puppet-code deploy --all --wait
    ```

### Create a new environment:
1. Clone the production branch
1. Syncronize data from your primary:
    ```bash
    $ puppet-code deploy --all --wait
    ```

### Delete an environment:
1. Remove branch (environment) from git.
1. Syncronize data from your primary:
    ```bash
    $ puppet-code deploy --all --wait
    ```
   
# Code Manager

[INDEX](../../README.md)

## Overview
Code manager syncronize local environments (branches) using a remote git repo. it use r10k and file sync service to provide a consistent way to sync the code. Code manager use a code-staging folder where r10k deploy the code and then use file sync service to copy the data to the "code" directory.

### Configure code manager:

1. Create a keypar to be used to syncronize with your GIT repo:
    ```bash
    $ ssh-keygen -t rsa -b 2048 -P '' -f /etc/puppetlabs/puppetserver/ssh/id-control_repo.rsa
    $ puppet infrastructure configure    # Set permissions to pe-puppet user
    ```
1. add the pub key to the repo and read/write permissions.
1. In the console, in the **PE Master** node group, set parameters:
   1. code_manager_auto_configure = true
   2. r10k_remote = "git@<YOUR.GIT.SERVER.COM>:puppet/control-repo.git"
   3. r10k_private_key = "/etc/puppetlabs/puppetserver/ssh/id-control_repo.rsa"
1. Run Puppet on your primary server and all compilers:
    ```bash
    $ puppet agent -t
    ```

### Set up authetication for code manager:
To securely deploy environments, Code Manager needs an authentication token.

1. Assign a user to the deployment role or create a new one and assign to deployment role.
1. Create a new password if the user is new.
1. Issue the following command (with user/pass selected before) to get a token:
    ```bash
    $ puppet-access login --lifetime 180d
    ```
1. The default location for storing the token is ~/.puppetlabs/token. 
1. To view the token, run:
    ```bash
    $ bash puppet-access show
    ```

### Test code deployment:
1. Syncronize data from your primary:
    ```bash
    $ puppet-code deploy --dry-run
    --dry-run implies --wait.
    --dry-run implies --all.
    Dry-run deploying all environments.
    Found X environments.
    ```
   
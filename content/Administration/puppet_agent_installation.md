# Puppet agent installation

[INDEX](../../README.md)

## Add installation class to PE Master:
1. This step is **optional**: in order to get the installation steps for your agent node, if the node architecture and/or OS operating differs from the PE mastes it is neccesary to add a new class to the puppet enterprise:
    - Add Archictecture (Ubuntu, Redhat, etc) to PE master classification (Optional):
       1. Go to web console -> Configure -> Classification -> All Nodes -> PE infraestructure -> PE Master
       1. Inside this tab, go to Configuration.
       1. fill the field "add new class" with pe_repo::platform::(REDHAT|UBUNTU)
       1. once added, run a "puppet agent -t" in the master node.
1. Open the web console and go to **"setup -> unsigned certifcates"** and grab the installation URL and run on the agent. It will be something similar to this:
   ```bash
    $ curl -k https://puppet-master-node:8140/packages/current/install.bash | sudo bash
   ```
1. Once the installation script finished, check the agent fingerprint on the agent:
    ```bash
    $ puppet agent --fingerprint
    (SHA256) 9E:F0:60:5B:6D:9B:00:AE:CE:69:7C:5F:5E:FD:6E:55:BF:1B:50:8E:F4:52:43:37:43:9A:47:5B:FF:BA:AA:A1
    ```
1. Compare this fingerprint with the received in the console:
    - go to **"SETUP -> Unsigned certifcates"**.

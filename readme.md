# Ansible Scripts for Deploying Multi-Cluster Hadoop

These Ansible scripts install Multi-Clustered Hadoop setups.  

Currently only Debian based systems are supported.

The software version matrix which will be installed is as follows:

| Software | Version |
|----------|---------|
| Hadoop   | 2.10.2  |
| Java     | 8       |

### Quick Installation
1. Edit the `hosts` file in the root directory:
    ```conf
    [group-name] => master or workers
    <public-ip-address>   hostname=<arbitrary-hostname> internal_ip=<internal-ip>

    Example:
    [master]
    x.x.x.x       hostname=node-master    internal_ip=10.0.0.x
    [workers]
    x.x.x.x       hostname=node1          internal_ip=10.0.0.x
    x.x.x.x       hostname=node2          internal_ip=10.0.0.x
    ```

Make sure that you can SSH into these VMs

2. Run the playbook
    ```bash
    ansible-playbook main.yml
    ```

### Notes
- These scripts will deploy Multi-Cluster Hadoop on VMs
- All the communication between the nodes in the cluster will happen via the internal network, using their internal_ip(s)
- The hostnames are arbitrary names which will be paired with the internal IP and appended to every node's `/etc/hosts`.

### Tips
- In order to prevent leaking hosts, order git to consider it always updated:
    ```bash
    git update-index --skip-worktree hosts
    ```

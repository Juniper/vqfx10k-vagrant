
This Vagrantfile will spawn 2 instances of VQFX (light)  
Both VQFX will be connected back to back with IP address pre-configured on their interfaces

# Requirement

### Resources
 - RAM : 2G
 - CPU : 1 Core (shared)

### Tools
 - Ansible for provisioning (except for windows)
 - Junos module for Ansible

# Topology

        em0|                        em0|
    =============               =============
    |           |  em3 - em7    |           |
    |   vqfx1   | ------------- |   vqfx2   |
    |           | ------------- |           |
    =============               =============

# Provisioning / Configuration

Ansible is used to preconfigured both VQFX with an IP address on their interfaces

If you don't have ansible or if ansible is not working you can start the topology without Ansible
```
vagrant up --no-provision
```

Later it's possible deploy all configuration
```
vagrant provision
```

Once the topology has been provisioned at least once, Vagrant will create a topology file corresponding to your topology.
The project is configured to automatically use this file, it's possible to call any playbook manually.  
```
ansible-playbook pb.conf.all.commit.yaml
```

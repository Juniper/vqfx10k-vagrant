
This Vagrantfile will create an IP Fabric composed of 2 spine and 3 leaf devices with 1 server attached to each leaf.
Overall it will spawn 5 instances of VQFX (light) and 3 Ubuntu servers.

The configuration of the Junos devices can be done using Ansible.
# Requirement
### Resources
 - RAM : 7G
 - CPU : 2 Core (shared)

### Tools
 - Ansible for provisioning (except for windows)
 - Junos module for Ansible

# Topology

Spine / Leaf topology with
- 2 spine
- 3 leaf
- 3 servers

# Provisioning / Configuration

Ansible is used to preconfigured all VQFX with an IP address on their interfaces
Both servers are preconfigured with an IP address and a route to their respective vQFX

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


This Vagrantfile will create an IP Fabric composed of 2 spine and 3 leaf devices with 1 server attached to each leaf.
Overall it will spawn 5 instances of vQFX (full - each with 1 Routing Engine VM and 1 PFE VM) and 3 Ubuntu servers.

Ansible used to configure devices.

# Requirements
### Resources
 - RAM : 16G
 - CPU : 4 Core (shared)

### Tools
 - Ansible for provisioning (except for windows)
 - Juniper.junos role for Ansible
 - junos-eznc python module (Junos PyEZ)

# Topology

Spine / Leaf topology with
- 2 spine
- 3 leaf
- 3 servers
```
                     ==============              ==============
                     | spine1-pfe |              | spine2-pfe |
                     ==============              ==============
                         em1|                        em1|
                     ==============               ==============
                     |            |               |            |
                     | spine1-re  |               | spine2-re  |
                     |            |               |            |
                     ==============               ==============
                   xe-0/0/0 - xe-0/0/2          xe-0/0/0 - xe-0/0/2
                                                                           
    xe-0/0/0 - xe-0/0/1          xe-0/0/0 - xe-0/0/1          xe-0/0/0 - xe-0/0/1
      ==============               ==============               ==============
      |            |xe-0/0/2       |            |xe-0/0/2       |            |xe-0/0/2
      | leaf1-re   |-------        |  leaf2-re  |-------        |  leaf3-re  |-------
      |            |      |        |            |      |        |            |      |
      ==============      |        ==============      |        ==============      |
           em1|           |            em1|            |           em1|             |
      ==============      |        ==============      |        ==============      |
      | leaf1-pfe  |      |        | leaf2-pfe  |      |        | leaf3-pfe  |      |
      ==============      |        ==============      |        ==============      |
                          |                            |                            |
                          |                            |                            |
                      eth1|192.168.1.2             eth1|192.168.2.2             eth1|192.168.3.2
                      =========                    =========                    =========
                      | srv1  |                    | srv2  |                    | srv3  |
                      =========                    =========                    =========
```

## Interfaces (traffic stats are shown on em interfaces, not xe interfaces.)
### vqfx10k-re:
- em0 - oob mgmt interface.
- em1 - Internal link to connect RE to PFE. Same interface on both RE and PFE.
- em2 - Not used.
- em3-em5 (xe-0/0/0-xe-0/0/2) - Used for interconnecting switches.

### vqfx10k-pfe:
- em0 - oob mgmt interface. 
- em1 - Internal link to connect RE to PFE. Same interface on both RE and PFE.

# Provisioning / Configuration

Ansible is used to preconfigure all vQFX with an IP address on their interfaces.
Servers are preconfigured with an IP address and a route to their respective vQFX.

If you don't have ansible or if ansible is not working you can start the topology without Ansible
```
vagrant up --no-provision
```

Later it's possible to deploy all configuration
```
vagrant provision
```

Once the topology has been provisioned at least once, Vagrant will create a topology file corresponding to your topology.
The project is configured to automatically use this file, it's possible to call any playbook manually.  
```
ansible-playbook pb.conf.all.commit.yaml
```

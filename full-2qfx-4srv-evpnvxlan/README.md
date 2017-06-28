***
This Vagrantfile will spawn 2 instances of VQFX (Full) each with 1 Routing Engine and 1 PFE VM  
We will also spawn 2 server VMs pre-configured with IP's on the same subnet.

Both VQFX will be connected back to back with IP address pre-configured on their interfaces
Underlay control plane is pre-configured using OSPF.
Overlay control plane with EVPN is pre-configured.
Ansible used to configure devices.


## Interfaces (traffic stats are shown on em interfaces, not xe interfaces.)
### vqfx10k-re:
em0 - oob mgmt interface 
em1 - Internal link to connect RE to PFE. Same interface on both RE and PFE.
em2 - Not used
em3 - xe-0/0/0 - Used for interconnecting switches
em4 - xe-0/0/1 
em5 - xe-...
em6 - ...

### vqfx10k-pfe:
em0 - oob mgmt interface 
em1 - Internal link to connect RE to PFE. Same interface on both RE and PFE.

# Requirements

### Resources
 - RAM : 8G
 - CPU : 3 (PFE VMs are capped to 50% CPU usage)

### Tools
 - Ansible for provisioning (except for windows)
 - Junos module for Ansible

# Topology

EVPN preconfigured
VXLAN connecting servers pre-configured
Servers pre-configured

      10.10.1.10 10.10.2.10      10.10.1.20 10.10.2.20
      ========= =========        ========= =========
      | srv11 | | srv12 |        | srv21 | | srv22 |
      ========= =========        ========= =========
        eth1 |   | eth1            eth1 |   | eth1
    xe-0/0/1 |   | xe-0/0/2    xe-0/0/1 |   | xe-0/0/2
      =============               =============
      |           | ------------- |           |
      | vqfx1-re  |    xe-0/0/0   | vqfx2-re  |
      |           |               |           |
      =============               =============
          em1|                        em1|
      =============               =============
      | vqfx1-pfe |               | vqfx1-pfe |
      =============               =============

# Provisioning / Configuration

Ansible is used to preconfigured both VQFX with an IP address on their interfaces

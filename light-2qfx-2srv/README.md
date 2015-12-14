
This Vagrantfile will spawn 2 instances of VQFX (light) and 2 Ubuntu servers
Both VQFX will be connected back to back with IP address  and eBGP pre-configured on their interfaces

# Requirement
### Resources
 - RAM : 3G
 - CPU : 1 Core (shared)

### Tools
 - Ansible for provisioning (except for windows)
 - Junos module for Ansible

# Topology

        em0|                        em0|
    =============               =============
    |           |  em4 em5      |           |
    |   vqfx1   | ------------- |   vqfx2   |
    |           | ------------- |           |
    =============               =============
        em3|                        em3|
    =============               =============
    |    srv1   |               |    srv2   |
    =============               =============

# Provisioning / Configuration

Ansible is used to preconfigured both VQFX with an IP address on their interfaces
Both servers are preconfigured with an IP address and a route to their respective vQFX

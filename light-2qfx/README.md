
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
    |           |  em4 em5      |           |
    |   vqfx1   | ------------- |   vqfx2   |
    |           | ------------- |           |
    =============               =============

Interface em3 is preconfigured and available to connect to external resources

# Provisioning / Configuration

Ansible is used to preconfigured both VQFX with an IP address on their interfaces

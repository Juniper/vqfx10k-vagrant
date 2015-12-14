
This Vagrantfile will spawn 1 instances of VQFX (light)  

# Requirement

### Resources
 - RAM : 1G
 - CPU : 1 Core (shared)

# Topology

        em0|      
    =============
    |           |
    |   vqfx1   |
    |           |
    =============

Interface em3 to em8 are all connected to the bridge "segment"

# Provisioning / Configuration

No provisioning used in this project


This Vagrantfile will spawn 1 instances of VQFX (Full) and 1 ubuntu server

# Requirement

### Resources
 - RAM : 3G
 - CPU : 2 Cores

# Topology

        em0|                        em0|
    =============  xe-0/0/0     =============
    |           | ------------- |   srv     |
    |   vqfx    |               =============
    |           |                
    =============              
        em1|                  
    =============             
    | vqfx-pfe  |             
    =============             

# Provisioning / Configuration

No provisioning used in this project


This Vagrantfile will spawn 1 instance of VQFX (Full)

# Requirement

### Resources
 - RAM : 3G
 - CPU : 2 Cores

# Topology

        em0|                       
    =============  
    |           |
    |   vqfx    |
    |           |                
    =============              
        em1|                  
    =============             
    | vqfx-pfe  |             
    =============             

# Provisioning / Configuration

No provisioning used in this project

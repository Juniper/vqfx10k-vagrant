
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

Both vqfx and srv will be preconfigured with Ip addresses


- vqfx: Ansible is used to configure interface xe-0/0/0 with IP 10.1.2.1
- srv: shell is used to configure interface eth1 with IP 10.1.2.2 

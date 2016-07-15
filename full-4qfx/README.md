
This Vagrantfile will spawn 4 instances of VQFX (Full) each with 1 Routing Engine and 1 PFE VM  
All VQFX will be interconnected in a full-mesh

> __This topology is a work in progress__

# Requirement

### Resources
 - RAM : 10G
 - CPU : 5 Cores

### Tools

# Topology

All devices are connected in Full-mesh with the following mapping 

```
vqfx1 xe-0/0/0   <>  vqfx4 xe-0/0/0	
vqfx1 xe-0/0/1   <>  vqfx3 xe-0/0/0
vqfx1 xe-0/0/2   <>  vqfx2 xe-0/0/0
vqfx2 xe-0/0/1   <>  vqfx4 xe-0/0/1
vqfx2 xe-0/0/2   <>  vqfx3 xe-0/0/1
vqfx3 xe-0/0/2   <>  vqfx4 xe-0/0/2
```

# Provisioning / Configuration

Not available yet

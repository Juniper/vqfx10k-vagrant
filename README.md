

# Requirement

 - Virtualbox version XXXX
 - Vagrant version XXXX

 To be confirmed ?
 - Ansible
 - Junos module for Ansible


```
apt-get install ansible
ansible-galaxy install Juniper.junos
```

# vQFX10K architecture and limitations

vqfx10k for Vagrant require 2 VMs for each instance
 - 1 Routing Engine VM, running Junos (add box name)
 - 1 Packet Forwarding Engine, running Linux (add box name)

These 2 VMS need to be interconnected with a dedicated private network on their interface number 1, interface 0 is always reserved for Vagrant for the management.

All dataplane ports need to be connected to the Routing Engine (RE) VM, up to 12 dataplane ports are supported.

### Limitations

#####vqfx10k-re

Require - 1G of memory
Interfaces type must be type : 82540EM

a maximum of 15 interfaces

#####vqfx10k-pfe

Require 1/2G of memory


# Install Box file locally

In case Vagrant Box are not available on Vagrant Cloud, you'll have to install them manually first

You can install a box with the command
```
vagrant box add {box name} {box path}
```

Both vqfx10k-re and vqfx10k-pfe need to be installed
```
vagrant box add juniper/vqfx10k-re /{path to box file}/vqfx10k-re-virtualbox.box
vagrant box add juniper/vqfx10k-pfe /{path to box file}/vqfx10k-pfe1-virtualbox.box  
```

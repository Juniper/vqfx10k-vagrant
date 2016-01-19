
This repository is a library of examples/demo using Vagrant and vqfx10K.  
Each example has its own directory and will contain at least a Vagrantfile

>during the beta, you have to install both images first, [instruction are available here](https://github.com/Juniper/vqfx10k-vagrant#install-box-file-locally) and [images are available here](https://github.com/Juniper/vqfx10k-vagrant/releases/tag/v0.2-beta)

To try an example, you just have to go inside a specific directory and do "vagrant up"
```
git clone https://github.com/Juniper/vqfx10k-vagrant.git
cd vqfx10k-vagrant/light-2qfx
vagrant up
```
Once both VM are up and running you can connect to them with
```
vagrant ssh vqfx1
vagrant ssh vqfx2
```

Available examples
- [full-1qfx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/full-1qfx)
- [full-1qfx-1srx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/full-1qfx-1srv)
- [full-2qfx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/full-2qfx)
- [light-1qfx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/light-1qfx)
- [light-2qfx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/light-2qfx)
- [light-2qfx-2srx](https://github.com/Juniper/vqfx10k-vagrant/tree/master/light-2qfx-2srx)

# How to contribute

Contribution to this repository are welcome and encouraged, especially to:
- Enhance the documentation of existing example
- Enhance existing example
- Create new example

### Guideline to create a new example

TODO

### How to provide feedback or report issue

The best solution to provide feedback is to open a new issue on the [github tracker](https://github.com/Juniper/vqfx10k-vagrant/issues) associated with this repo.  

Before opening a new issue, check the [troubleshooting guide - work in progress](https://github.com/Juniper/vqfx10k-vagrant/wiki/Troubleshooting-Guide)

# vQFX10K

vqfx10k is a tool provided for lab and training, this is not a intended to be used in production.
Capacities are similar to a real QFX10K but performance are very limited in this version.

## Mode, Architecture and Limitations

vqfx10k for Vagrant can work in 2 modes : **Full** and **Light**

### Mode Full
In mode full, it require 2 VMs for each instance
 - 1 Routing Engine VM, running Junos (vqfx10k-re-virtualbox.box)
 - 1 Packet Forwarding Engine, running Linux (vqfx10k-pfe-virtualbox.box)

>In mode Full, the dataplane is fully functional and is very close to the real QFX10K

These 2 VMS need to be interconnected with a dedicated private network on their interface number 1, (interface 0 is always reserved for Vagrant for the management).
All data-plane ports need to be connected to the Routing Engine (RE) VM, up to 12 data-plane ports are supported.
Ports name will be xe-0/0/0 to xe-0/0/11

#### Limitations in Mode full
Only few features are not supported due to some architecture differences between vQFX10K and a real QFX10K

Not supported features:
 - Analytics
 - Guest VM/ Guest container
 - EVPN

### Mode Light

In mode light, only 1 Routing Engine VM, running Junos is required for each instance

>In this mode, most dataplane features are not supported and all packets are processed in Kernel

Up to 12 ports are supported to connect to external devices, ports name will be em3 to em14

#### Limitations in mode light
In this mode, most dataplane features are not supported and all packets are processed in Kernel

- To be confirmed -
Family ethernet-switching is not supported

### VM Caracteristics

#### vqfx10k-re

Require - 1G of memory
Interfaces type must be type : 82540EM

A maximum of 15 interfaces are supported:
- first interface is used by vagrant (em0)
- second interface is used to connect to the PFE VM (em1)
- third interface is a management port not used (em2)
- All remaining interfaces can be used to connected to other devices

This VM has 2 account by default:
- login: vagrant, with ssh_key authentification using vagrant insecure_key
- login: root, password: Juniper

#### vqfx10k-pfe

Require:
- 1.5G of memory
- 1 dedicated core

A maximum of 2 interfaces are supported:
- first interface is used by vagrant (eth0)
- second interface is used to connect to the RE VM (eth1)

This VM has 2 account by default:
- login: vagrant, with ssh_key authentication using vagrant insecure_key
- login: root, password: no

# Vagrant

*What is Vagrant*
Vagrant is an open-source (MIT) tool for building and managing virtualized development environments developed by Mitchell Hashimoto and John Bender.
Vagrant is able to create VMs, connect them together and is specify configure them automatically.  
Here is a good [introduction to Vagrant for Network Engineer](https://www.dravetech.com/blog/2016/01/08/vagrant-for-network-engineers.html)

## providers
For now, only Virtualbox is supported as a provider
Vmware will be added soon  

# How to install and Requirement

## Requirements
 - Virtualbox, version 5.0.10 minimum
 - Vagrant, version 1.7 minimum

For Linux and MacOS, some examples require:
 - Ansible
 - Junos module for Ansible

#### How to install Ansible on MacOS
```
sudo easy_install pip
sudo pip install ansible
sudo ansible-galaxy install Juniper.junos
sudo pip install junos-eznc
```

#### How to install Ansible on Ubuntu/Linux
```
apt-get install ansible
ansible-galaxy install Juniper.junos
```

#### How to install Ansible for Windows

http://www.azavea.com/blogs/labs/2014/10/running-vagrant-with-ansible-provisioning-on-windows/

## Install Box file locally

In case Vagrant Box are not available on Vagrant Cloud, you'll have to install them manually first.

You can install a box with the command
```
vagrant box add {box name} {box path}
```

Both vqfx10k-re and vqfx10k-pfe need to be installed
```
vagrant box add juniper/vqfx10k-re /{path to box file}/vqfx10k-re-virtualbox.box
vagrant box add juniper/vqfx10k-pfe /{path to box file}/vqfx10k-pfe1-virtualbox.box  
```

During Alpha/Beta box files are available [on Github](https://github.com/Juniper/vqfx10k-vagrant/releases/tag/v0.2-beta)

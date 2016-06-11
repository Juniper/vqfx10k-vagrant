# Installation Guide

## Requirements
 - VirtualBox, version 5.0.10 minimum
 - Vagrant, version 1.7 minimum

> it's expected to NOT WORK with vagrant 1.5.x; 1.6.x etc ..
> Please check your version and upgrade manually if needed, for ubuntu it's easy to upgrade the package manually. See below  

For Linux and MacOS, some examples require:
 - Ansible
 - Junos module for Ansible

> Ansible is used to provision Junos VM automatically

## 1. Download and Install Vagrant and VirtualBox

#### Vagrant
Download > https://www.vagrantup.com/downloads.html

#### Virtualbox
Download > https://www.virtualbox.org/wiki/Downloads

> If you are using an _old_ version of linux (Ubuntu 14.04, 14.10 etc .. ) most likely **the version installed with apt-get will not work**
> In this case you need to update the version manually  
> for ubuntu :
> ```
> wget https://releases.hashicorp.com/vagrant/1.8.1/vagrant_1.8.1_x86_64.deb
> sudo dpkg -i vagrant_1.8.1_x86_64.deb
> ```

## 2. Install vqfx Box file locally

Because vqfx10k boxes are not available on Vagrant Cloud] yet, you'll have to install them manually first.

You can install a box with the command
```
vagrant box add {box name} {box path}
```

Both vqfx10k-re and vqfx10k-pfe need to be installed
```
vagrant box add juniper/vqfx10k-re /{path to box file}/vqfx10k-re-virtualbox.box
vagrant box add juniper/vqfx10k-pfe /{path to box file}/vqfx10k-pfe1-virtualbox.box  
```

> For now, Boxes are not yet available publicly, please contact your Juniper SE to add for access

## 3. (optional) Install Ansible
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

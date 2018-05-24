# Installation Guide for Windows Users

Because Ansible doesn't currently support Windows as a control machine, there are some extra steps that need to be done to make it work for Windows users. Once the installation process is finished, everything will run with a simple 'vagrant up' command. This will use the Windows Subsystem for Linux (WSL) to allow us to use Windows as our Ansible control machine.

There are many pre-built labs available publicly on GitHub that you can download on to your local machine. With the prebuilt EVPN-VXLAN lab you can view configurations and thoroughly understand all the building steps needed in a risk free environment. 


##Installation - Please follow steps in order

1. Install VirtualBox for Windows
	* This is a hypervisor that allows us to run vQFX in a virtual machine. For Virtualbox, you can find the download as well as installation instructions here https://www.virtualbox.org/wiki/Downloads (if you’re running Windows 10 you may need to turn off Hyper-V functionality in Windows Features and turn on Virtualization in the BIOS).
	
2. Install the Windows Subsystem for Linux
	* Turn on Developer Mode and follow this document https://docs.microsoft.com/en-us/windows/wsl/install-win10. You'll need to restart your computer.
	* Open the CLI by going to Run and typing 'cmd'
	* In the CLI type 'bash'
	* Follow the wizard to accept and input username and password. This essentially loads Ubuntu Linux on your Windows machine.
	
3. Install python-pip in WSL (Windows Subsystem for Linux)
	*  sudo apt-get install python-pip
	
4. Install Ansible in WSL
	* sudo pip install ansible
	* For some reason using apt-get to install Ansible installs an older version which is not compatible with some of the Ansible modules being run. Pip will install a more recent version (above 2.1).
	
5. Install PyEZ in WSL
	* Follow the directions here to install dependencies and PyEZ https://www.juniper.net/documentation/en_US/junos-pyez/topics/task/installation/junos-pyez-server-installing.html
	* This is required to run the juniper_junos_config module used in the Playbook.
	
6. Install jxmlease in WSL
	* pip install jxmlease
	
7. Install ncclient in WSL
	* pip install ncclient
	
8. Install Vagrant in WSL
	* wget https://releases.hashicorp.com/vagrant/2.1.1/vagrant_2.1.1_x86_64.deb
	* sudo dpkg -i vagrant_2.1.1_x86_64
	* export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
	* export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
	* Typing those environment variables into the WSL is the only thing that will let you communicate with VirtualBox which is installed in Windows. See this for more information https://www.vagrantup.com/docs/other/wsl.html.
	
9. Download the vqfx10k-vagrant project from GitHub in WSL
	* git clone https://github.com/Juniper/vqfx10k-vagrant
	
	
10. Go to the correct directory in WSL
	* cd vqfx10k-vagrant/full-2qfx-4srv-evpnvxlan
	* This directory contains multiple files including configuration and vagrant files that will help you spin up virtual machines and devices automatically, to simulate EVPN-VXLAN on your local machine.
	
11. Install the Juniper.junos role in WSL
	* sudo ansible-galaxy install Juniper.junos
	* The Juniper.junos role allows us to use functions specifically for Junos devices. If you experience any errors that mention this role, or point to juniper_junos_config, it's likely it's a problem with this role. Make sure it's either in the same directory where you're running 'vagrant up' or your ansible.cfg file points to it.
	
12. Use Vagrant to spin up devices
	* vagrant up
	* After typing 'vagrant up' devices will start spinning up in VirtualBox. VirtualBox does not need to be open, but you can open it to monitor status.
	* The vagrant file will also call Ansible to configure the devices. 
	* This may take several minutes to bring up four virtual servers and two vQFXs on your local machine, especially if it's the first time you've run it because it will need to download everything.

	



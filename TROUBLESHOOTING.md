
# I'm able access the VM with SSH but I don't have the password for "vagrant"

The user **vagrant** do not have a password, it’s using SSH-key only
The idea of Vagrant is that it will hide all that for you
While in your directory, you just have to do __vagrant ssh vqfx__ (vqfx being the name of the VM) to connect in SSH.
If you need to ssh directly, you can use the user **root** with **Juniper** as password
Everything is indicated on the [README](README.md) :)

# In Full mode, Check connectivity between RE and PFE VMs

Both VMs must be able to reach each other over IP
 - RE VM has IP : 169.254.0.2
 - PFE VM has IP : 169.254.0.1

From RE VM
```
vagrant@vqfx-re> ping 169.254.0.1
PING 169.254.0.1 (169.254.0.1): 56 data bytes
64 bytes from 169.254.0.1: icmp_seq=0 ttl=64 time=1.078 ms
```
From PFE VM
```
localhost:~$ ping 169.254.0.2
PING 169.254.0.2 (169.254.0.2) 56(84) bytes of data.
64 bytes from 169.254.0.2: icmp_seq=1 ttl=64 time=0.589 ms
```

# RE and PFE VMs are not able to communicate to each other, ping is not working

### Check if IPs are properly configured on both side
On RE VM  
Interface must be up with IP 169.254.0.2
```
vagrant@vqfx-re> show interfaces terse | grep em1
em1                     up    up
em1.0                   up    up   inet     169.254.0.2/24
```

On PFE VM  
You need to go in Root and see check if eth1 interface is UP and has IP
Root password is **no**
```
ocalhost:~$ su - root
Password:
root@localhost:~# ifconfig eth1
eth1      Link encap:Ethernet  HWaddr 08:00:27:5c:5c:09
          inet addr:169.254.0.1  Bcast:169.254.0.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe5c:5c09/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:768417 errors:0 dropped:0 overruns:0 frame:0
          TX packets:341681 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:74964712 (71.4 MiB)  TX bytes:26401230 (25.1 MiB)
```

# RE and PFE VMs are able to communicate but XE interfaces are not present

This might happen if we are running our of CPU
You might want to allocate less CPU resources to PFE VMs  
In the Vagrantfile, you can add
```yaml
            vqfxpfe.vm.provider "virtualbox" do |v|
                v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
            end
```



# Install Box file locally

In case Vagrant Box are not available on Vagrant Cloud, you'll have to install them manually first

You can install a box with the command
```
vagrant box add {box name} {box path}
```

Both vqfx10k-re and vqfx10k-pfe need to be installed
```
vagrant box add vqfx10k-re /{path to box file}/vqfx10k-re-virtualbox.box
vagrant box add vqfx10k-pfe /{path to box file}/vqfx10k-pfe1-virtualbox.box  
```

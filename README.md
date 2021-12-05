# vagrant-templates


```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|
   # Create bootstrap.sh script for global 
  config.vm.provision "shell", path: "bootstrap.sh"

  # Template for Servers
  config.vm.define "template" do |node|
  
    node.vm.box               = "generic/ubuntu2104"
    node.vm.box_check_update  = false
    node.vm.box_version       = "3.3.0"
    node.vm.hostname          = "template.example.com"

    node.vm.network "private_network", ip: "172.16.16.30"
    node.vm.network "private_network", ip: "192.168.122.30"
    node.vm.network "forwarded_port", guest: 22, host: 8022
  
    node.vm.provider :virtualbox do |v|
      v.name    = "tempalte"
      v.memory  = 2048
      v.cpus    =  2
    end  
    # Create bootstrap_template.sh for node particular
    node.vm.provision "shell", path: "bootstrap_template.sh"
  end
end
```

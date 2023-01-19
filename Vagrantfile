# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config| 

    config.vm.define "host1" do |host1|
      host1.vm.box = 'centos/7'
    
      host1.vm.host_name = 'host1.test.local'
      host1.vm.network "private_network", ip: "192.168.56.240"
      host1.vm.network "forwarded_port", guest: 80, host: 8080
      
      host1.vm.provider "virtualbox" do |vb|
        vb.memory = "4096"
        vb.cpus = "3"
      end
      end
       
      config.vm.define "host2" do |host2|
        host2.vm.box = 'centos/7'
    
        host2.vm.host_name = 'host2.test.local'
        host2.vm.network "private_network", ip: "192.168.56.241"
        host2.vm.network "forwarded_port", guest: 80, host: 8081
        end
end


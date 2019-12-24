# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
  end
  config.vm.define "netdata" do |netdata|
    netdata.vm.box = "hashicorp/bionic64"
    netdata.vm.hostname = "netdata"
    netdata.vm.network "private_network", type: "dhcp"
  end
  config.vm.define "machine1" do |machine1|
    machine1.vm.box = "hashicorp/bionic64"
    machine1.vm.hostname = "machine1"
    machine1.vm.network "private_network", type: "dhcp"
  end
  config.vm.define "machine2" do |machine2|
    machine2.vm.box = "hashicorp/bionic64"
    machine2.vm.hostname = "machine2"
    machine2.vm.network "private_network", type: "dhcp"
  end
  config.vm.define "machine3" do |machine3|
    machine3.vm.box = "hashicorp/bionic64"
    machine3.vm.hostname = "machine3"
    machine3.vm.network "private_network", type: "dhcp"
    machine3.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.limit = "all"
      ansible.groups = {
        "netdata_master" => ["netdata"],
        "web" => ["machine1", "machine2"],
        "database" => ["machine3"],
        "netdata_slaves:children" => ["web", "database"],
        "netdata_servers:children" => ["netdata_master", "netdata_slaves"]
      }
    end
  end
end

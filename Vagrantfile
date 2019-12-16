# -*- mode: ruby -*-
# vi: set ft=ruby :

NETDATA_IP = "172.28.128.11"
MACHINE1_IP = "172.28.128.12"
MACHINE2_IP = "172.28.128.13"
MACHINE3_IP = "172.28.128.14"

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

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end

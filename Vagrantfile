# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<-SCRIPT
  apt-get update
  apt-get install -y --fix-missing python-minimal software-properties-common sshpass build-essential python python-pip apt-transport-https ca-certificates libffi-dev libssl-dev python-apt
  pip install pip --upgrade
  pip install setuptools --upgrade
  pip pyopenssl ndg-httpsclient pyasn1

  pip install ansible
SCRIPT

$script_python = <<-SCRIPT
  apt-get update
  apt-get install -y --fix-missing software-properties-common sshpass python-minimal sshpass python build-essential apt-transport-https ca-certificates libffi-dev libssl-dev python-apt
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.define "acs" do |acs|
    acs.vm.box = "ubuntu/xenial64"
    acs.vm.hostname = "acs"
    acs.vm.network "private_network", ip: "192.168.33.10"
    acs.vm.synced_folder "./data/ansible", "/home/vagrant/ansible"
    acs.vm.provision "shell", inline: $script
  end

  config.vm.define "loadbalancer" do |loadbalancer|
    loadbalancer.vm.box = "ubuntu/xenial64"
    loadbalancer.vm.hostname = "loadbalancer"
    loadbalancer.vm.network "private_network", ip: "192.168.33.20"
    loadbalancer.vm.provision "shell", inline: $script_python
  end

  config.vm.define "blue" do |blue|
    blue.vm.box = "ubuntu/xenial64"
    blue.vm.hostname = "blue"
    blue.vm.network "private_network", ip: "192.168.33.30"
    blue.vm.provision "shell", inline: $script_python
  end

  config.vm.define "green" do |green|
    green.vm.box = "ubuntu/xenial64"
    green.vm.hostname = "green"
    green.vm.network "private_network", ip: "192.168.33.40"
    green.vm.provision "shell", inline: $script_python
  end

  config.ssh.insert_key = false
  
end

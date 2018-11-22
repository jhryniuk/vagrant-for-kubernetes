# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
sudo apt-get --yes install software-properties-common python-pip > /dev/null 2>&1
sudo apt-add-repository --yes ppa:ansible/ansible > /dev/null 2>&1
sudo apt-get --yes update  > /dev/null 2>&1
sudo apt-get --yes install ansible
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.define "master01" do |v|
    v.vm.hostname = "master01"
    v.vm.box = "ubuntu/xenial64"
    v.vm.box_check_update = true

    v.vm.network "private_network", ip: "10.0.0.200"

    v.ssh.forward_agent = true
    v.vm.provider :virtualbox do |p|
      p.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      p.customize ["modifyvm", :id, "--memory", 2048]
      p.customize ["modifyvm", :id, "--name", "master"]
      p.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
      p.cpus = 1
    end

    v.vm.provision "shell", inline: $script
    v.vm.provision "ansible" do |ansible|
      ansible.playbook = "master.yaml"
      ansible.inventory_path = "./hosts"
      ansible.limit = "master"
    end
  end

  config.vm.define "node01" do |v|
    v.vm.hostname = "node01"
    v.vm.box = "ubuntu/xenial64"
    v.vm.box_check_update = true

    v.vm.network "private_network", ip: "10.0.0.201"

    v.ssh.forward_agent = true
    v.vm.provider :virtualbox do |p|
      p.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      p.customize ["modifyvm", :id, "--memory", 2048]
      p.customize ["modifyvm", :id, "--name", "node01"]
      p.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
      p.cpus = 1
    end

    v.vm.provision "shell", inline: $script
    v.vm.provision "ansible" do |ansible|
      ansible.playbook = "node.yaml"
      ansible.inventory_path = "./hosts"
      ansible.limit = "node01"
    end
  end

  config.vm.define "node02" do |v|
    v.vm.hostname = "node02"
    v.vm.box = "ubuntu/xenial64"
    v.vm.box_check_update = true

    v.vm.network "private_network", ip: "10.0.0.202"

    v.ssh.forward_agent = true
    v.vm.provider :virtualbox do |p|
      p.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      p.customize ["modifyvm", :id, "--memory", 2048]
      p.customize ["modifyvm", :id, "--name", "node02"]
      p.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
      p.cpus = 1
    end

    v.vm.provision "shell", inline: $script
    v.vm.provision "ansible" do |ansible|
      ansible.playbook = "node.yaml"
      ansible.inventory_path = "./hosts"
      ansible.limit = "node02"
    end
  end
end

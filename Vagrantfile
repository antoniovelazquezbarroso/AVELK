# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.define "logger" do |logger|
    logger.vm.box = "geerlingguy/ubuntu1404"
    logger.vm.hostname = "logger"    
    logger.vm.network :private_network, ip: "192.168.2.35"

    logger.vm.provision "ansible" do |ansible|
      ansible.playbook = "./playbooks/logger/playbook.yml"
      ansible.inventory_path = "./playbooks/logger/inventory"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end

  end

  config.vm.define "shipper" do |shipper|
    shipper.vm.box = "geerlingguy/ubuntu1404"
    shipper.vm.hostname = "shipper"    
    shipper.vm.network :private_network, ip: "192.168.2.40"

    shipper.vm.provision "ansible" do |ansible|
      ansible.playbook = "./playbooks/shipper/playbook.yml"
      ansible.inventory_path = "./playbooks/shipper/inventory"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end

  end

end

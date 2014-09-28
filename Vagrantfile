# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
settings = YAML.load_file('vars.yml')

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "Ubuntu_14.04_64_Server_Gui"
  config.vm.box_url = "https://dl.dropboxusercontent.com/u/23261942/Ubuntu_14.04_64_Server_Gui.box"
  config.vm.network "private_network", ip: settings["vagrant_vm_ip_address"]
  config.ssh.forward_agent = true
  config.vm.synced_folder "/Users/bdb/sites", "/srv/projects", owner: "vagrant", group: "vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = "vars.yml"
  end

end

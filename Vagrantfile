# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "hashicorp/precise64"

  config.vm.network "forwarded_port", guest: 9200, host: 9200, auto_correct: true
  config.vm.network "forwarded_port", guest: 9300, host: 9300, auto_correct: true
  config.vm.network "forwarded_port", guest: 9160, host: 9160, auto_correct: true
  config.vm.network "forwarded_port", guest: 7199, host: 7199, auto_correct: true

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "./srv", "/srv", :nfs => { :mount_options => ["dmode=775","fmode=664"] }

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "3072"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.sudo = true
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_path = "provisioning/hosts"
    #ansible.verbose = "vvvv"
    ansible.limit = 'all'
    ansible.host_key_checking = false
  end

end

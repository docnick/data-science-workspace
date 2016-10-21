# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(2) do |config|

  config.vm.define :dev, primary: true do |dev|
	dev.vm.box = "ubuntu/trusty64"

	dev.vm.network :private_network, ip: "33.33.33.200"
	dev.vm.network "forwarded_port", guest: 3306, host: 3306

	dev.vm.provider :virtualbox do |v|
	    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		v.customize ["modifyvm", :id, "--memory", "2048"]
	end

    dev.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "hosts"
	    ansible.sudo = true
		ansible.verbose = "vvvv"
        ansible.limit = "dev"
        ansible.playbook = "dev.yml"
    end
  end
  config.vm.synced_folder(".", "/home/vagrant/shared/")
end
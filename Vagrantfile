# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.network :forwarded_port, guest: 8000, host: 9000
  config.vm.network :forwarded_port, guest: 8001, host: 9001

  config.vm.network :private_network, ip: "192.168.20.40"

  nfs_setting = RUBY_PLATFORM =~ /darwin/ || RUBY_PLATFORM =~ /linux/
  config.vm.synced_folder ".", "/opt/edx/edx-platform", id: "vagrant-root", :nfs => nfs_setting
  config.ssh.forward_agent = true
  config.vm.provider :virtualbox do |vb|
   	
  vb.customize ["modifyvm", :id, "--memory", "2048"]
  vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision :shell, :path => "scripts/install-acceptance-req.sh"
  config.vm.provision :shell, :path => "scripts/vagrant-provisioning.sh"
end

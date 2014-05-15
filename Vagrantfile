# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  
  primary_password = 'vagr1234'
  hostname = 'vagrant-vm.local'

  # ensures the latest version of chef[-solo] is running
  config.omnibus.chef_version = :latest

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = 'precise64'
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: '192.168.200.10'

  config.vm.hostname = hostname

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # Lucky people can enable nfs but they will get permission errors https://groups.google.com/forum/?fromgroups=#!topic/vagrant-up/-J3UEqYXveA
  config.vm.synced_folder '.', '/vagrant', :mount_options => %w('dmode=777','fmode=777')

  config.vm.provider :virtualbox do |vb|

    vb.name = hostname

    # Use VBoxManage to customize the VM. For example to change memory:
    # vb.customize ['modifyvm', :id, '--memory', '1048']
    vb.customize ['modifyvm', :id, '--cpus', '2']
    vb.customize ['modifyvm', :id, '--natdnshostresolver1','on']
    vb.customize ['modifyvm', :id, '--natdnsproxy1','on']
  end

  config.vm.provision :chef_solo do |chef|

    #chef.environment = environment

    # Specify vagrant cookbooks: our project cookbooks and magento required cookbooks
    chef.cookbooks_path = %w(./recipes/site-cookbooks ./recipes/cookbooks)
    #chef.environments_path = './recipes/environments'
    #chef.add_recipe 'brightspot'

    # You may also specify custom JSON attributes:
    chef.json = {
    }
    chef.log_level = :debug

  end
end

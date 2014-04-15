# -*- mode: ruby -*-
# vi: set ft=ruby tw=2 ts=2 sw=2 sts=2:

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "parallels/centos-6.5"

  config.omnibus.chef_version = :latest

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "mysql_scripts", "/etc/mysql"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :parallels do |p|
    p.name = "mysql_centos"
    p.check_guest_tools = true
    p.memory = 1024
    p.cpus = 1
  end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  VAGRANT_JSON = JSON.parse(Pathname(__FILE__).dirname.join('nodes', 'mysql_server.json').read)

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :chef_solo do |chef|
    #chef.cookbooks_path = "./cookbooks"
    #chef.roles_path = "../my-recipes/roles"
    #chef.data_bags_path = "../my-recipes/data_bags"

    chef.run_list = VAGRANT_JSON.delete('run_list')
    chef.json = VAGRANT_JSON
  end

end

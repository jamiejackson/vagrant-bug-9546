# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # true = auto check/update vbox guest additions
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end
  
  ip = "192.168.56.95"
  server_hostname="my-host-name"
  docker_compose_version = "1.16.1"
  
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_version = "20180222.1.1"
  
  config.vm.hostname = server_hostname;

  # create a private network so the host can access the guest
  config.vm.network "private_network", ip: ip
  
  config.vm.provision "docker"
  config.vm.provision "docker_compose", compose_version: docker_compose_version


  config.vm.provision  :docker_compose,
    options: "-p docker",
    yml: ["/vagrant/docker-compose.yml"],
    command_options: { up: "-d --remove-orphans" },
    env: {},
    rebuild: true,
    run: "always",
    compose_version: docker_compose_version


end

# -*- mode: ruby -*-
# vi: set ft=ruby :

required_plugins = %w( vagrant-hostmanager )
required_plugins.each do |plugin|
  exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure(2) do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.box = "ubuntu/trusty64"

  config.vm.hostname = "shaktihealinggardens.local"

  config.vm.network "private_network", ip: "192.168.33.17"

  config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=777","fmode=777"]

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible.yml"
  end
end
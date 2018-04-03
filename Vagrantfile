# -*- mode: ruby -*-
# # vi: set ft=ruby :

# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Require YAML module
require 'yaml'

# Read YAML file with box details
servers = YAML.load_file('servers.yaml')

# Create boxes
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Iterate through entries in YAML file
  servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]
      srv.vm.synced_folder '.', '/vagrant', disabled: true
      srv.vm.hostname = servers["name"]
      srv.vm.network "private_network", ip: servers["ip"]
      #
      srv.vm.provider :libvirt do |libvirt|
        libvirt.memory = servers["ram"]
        #libvirt.cpus = servers["cpus"]
      end
    end
  end
end

#!/usr/bin/env ruby
# -*- coding: utf-8 -*-
# vi: set ft=ruby :

require 'etc'
require 'shellwords'

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # CentOS 7 VM
  config.vm.define "default", autostart: true, primary: true do |linux|
    # Every Vagrant virtual environment requires a box to build off of.
    linux.vm.box = "bento/centos-7.4"
    linux.vm.hostname = "devel"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    linux.vm.network "private_network", type: "dhcp"

    # Tweak the VMs configuration.
    linux.vm.provider "virtualbox" do |vb|
      vb.cpus = Etc.nprocessors
      vb.memory = 1024
      vb.linked_clone = true
    end

    # Configure the VM using Ansible
    linux.vm.provision "ansible_local" do |ansible|
      ansible.galaxy_role_file = "requirements.yml"
      ansible.galaxy_roles_path = ".ansible/galaxy-roles"
      ansible.provisioning_path = "/vagrant"
      ansible.playbook = "vagrant.yml"
      # allow passing ansible args from environment variable
      ansible.raw_arguments = Shellwords::shellwords(ENV.fetch("ANSIBLE_ARGS", ""))
    end
  end

  # macOS VM
  config.vm.define "mac", autostart: false do |macOS|
    macOS.vm.hostname = "macos"
    macOS.vm.box = "macOS/sierra"
    macOS.vm.box_url = "https://vagrant-osx.nyc3.digitaloceanspaces.com/osx-sierra-0.3.1.box"

    macOS.vm.network "private_network", "type": "dhcp"

    macOS.vm.provider "virtualbox" do |vb|
      vb.cpus = Etc.nprocessors
      vb.memory = 1024
      vb.linked_clone = true
    end

    macOS.vm.provision "ansible" do |ansible|
      ansible.galaxy_role_file = "tests/requirements.yml"
      ansible.galaxy_roles_path = ".ansible/galaxy_roles"
      # ansible.provisioning_path = "/vagrant"
      ansible.playbook = "macos.yml"
      # allow passing ansible args from environment variable
      ansible.raw_arguments = Shellwords::shellwords(ENV.fetch("ANSIBLE_ARGS", ""))
    end
  end
end

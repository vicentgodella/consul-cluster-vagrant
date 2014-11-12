# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.box_check_update = false

  config.ssh.forward_agent = true

  num_nodes = 3
  base_ip = "192.168.10."

  config.vm.provider "virtualbox" do |v|
    v.memory = 256
  end

  (1..num_nodes).each do |index|
    ip4       = index + 10
    ip_addr   = "#{base_ip}#{ip4}"
    hostname  = "consul#{index}"

    config.vm.define hostname do |node|
      node.vm.box       = "ubuntu/trusty64"
      node.vm.host_name = hostname
      node.vm.network "private_network", ip: ip_addr

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "consul.yml"
        ansible.inventory_path = "hosts_consul"
        ansible.host_key_checking = false
      end
    end
  end
end

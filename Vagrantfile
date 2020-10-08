# -*- mode: ruby -*-
# vi: set ft=ruby :

CEPH_NODES = 3

DISKS = 1
DISKSIZE = "50G"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  # config.vm.box = "fedora/31-cloud-base"

  config.vm.provider "libvirt" do |lv|
    lv.cpus = "2"
    lv.memory = "1024"
    # Always use system connection instead of QEMU session
    lv.qemu_use_session = false
  end

  # disable default sync dir
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Uncomment the below lines if you want dedicated ceph-admin node
  #config.vm.define "ceph-admin" do |node|
  #  node.vm.hostname = "ceph-admin"
  #  localoctet = 100+CEPH_NODES+1
  #  node.vm.network :private_network, ip: "192.168.50.#{localoctet}"
  #end

  (1..CEPH_NODES).each do |i|
    config.vm.define "ceph-node#{i}" do |node|
      node.vm.hostname = "ceph-node#{i}"
      localoctet = 100+i
      node.vm.network :private_network, ip: "192.168.50.#{localoctet}"
      node.vm.provider "libvirt" do |provider|
        for _ in 0..DISKS-1 do
          provider.storage :file, :size => DISKSIZE
        end
      end
      # Only execute the Ansible provisioner once,
      # when all the machines are up and ready.
      if i == CEPH_NODES
        node.vm.provision :ansible do |ansible|
          ansible.groups = {
            "ceph_nodes" => (1..CEPH_NODES).map {|j| "ceph-node#{j}"},
            # If you want a dedicated ceph-admin node,
            # modify 's/ceph-node1/ceph-admin/' at below line
            "ceph_admin" => ["ceph-node1"]
          }
          # Disable default limit to connect to all the machines
          ansible.limit = "all"
          ansible.playbook = "ansible/playbook.yml"
        end
      end
    end
  end
end

# ceph-cluster

### Basic usage
---

To bring up a basic multi-node ceph cluster, just run:

<pre>
$ vagrant up
</pre>

#### The goal:
---
* Initiate a `rbd block pool`, create an image
    * In the summary, provide instructions to map image and mount the device
* Create `ceph file system`
    * In the summary, provide clear instructions to mount the CephFs volume


#### Dedicated ceph-admin node:
---
Make below changes to your Vagrantfile for a dedicated ceph admin node, else by default one of the ceph cluster nodes will be choosen to run admin tasks

<pre>
Uncomment these lines
#config.vm.define "ceph-admin" do |node|
#  node.vm.hostname = "ceph-admin"
#  localoctet = 100+CEPH_NODES+1
#  node.vm.network :private_network, ip: "192.168.50.#{localoctet}"
#end

Also modify 's/ceph-node1/ceph-admin/' at below line
"ceph_admin" => ["ceph-node1"]
</pre>

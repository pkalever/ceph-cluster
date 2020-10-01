# ceph-cluster

### Basic usage
---

To bring up a basic multi-node ceph cluster, just run:

<pre>
$ vagrant up
</pre>

#### The goal:
---
* Initiate a `rbd block pool`, create an image, then map it and finally mount at '/mnt/rbd' path.
* Create `ceph file system` and mount it at '/mnt/cephfs' path.


#### Dedicated ceph-admin node:
---
Make below changes to your Vagrantfile for a dedicated ceph admin node, else by default one of the ceph cluster nodes will be choosen to run admin tasks

<pre>
Uncomment these lines
#config.vm.define "ceph-admin" do |node|
#  node.vm.hostname = "ceph-admin"
#end

Also modify 's/ceph-node1/ceph-admin/' at below line
"ceph_admin" => ["ceph-node1"]
</pre>

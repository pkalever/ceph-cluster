# ceph-cluster

### Basic usage
---

To bring up a basic multi-node ceph cluster, just run:

<pre>

$ vagrant up

</pre>

The goal:
* Initiate a `rbd block pool`, create an image, then map it and finally mount at '/mnt/rbd' path.
* Create `ceph file system` and mount it at '/mnt/cephfs' path.

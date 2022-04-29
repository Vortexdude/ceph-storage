# ceph-storage

`Ceph Storage` Cluster setup requires at least one `Ceph Monitor`, `Ceph Manager`, and `Ceph OSD` (Object Storage Daemon) and may be `Ceph Metadata` Server for providing Ceph File System Storage.

All these components perform various roles;

#### Ceph Admin node (`cephadm`)
It is the node on which Ceph deployment script (cephadm) is installed on.
Ceph Object Storage Daemon (OSD, ceph-osd)
It provides ceph object data store.
It also performs data replication , data recovery, rebalancing and provides storage information to Ceph Monitor.

#### Ceph Monitor (`ceph-mon`)
It maintains maps of the entire ceph cluster state including monitor map, manager map, the OSD map, and the CRUSH map.
manages authentication between daemons and clients

#### Ceph Manager (`ceph-mgr`)
keeps track of runtime metrics and the current state of the Ceph cluster, including storage utilization, current performance metrics, and system load.
manages and exposes Ceph cluster web dashboard and API.
At least two managers are required for HA.

### This ansible playbook is used for the setup the ceph-storage cluster


## about the plabook
This ansible plabook reuired one external devie is mounted on each node this is used to share data acroos cluster and this ansible role creating two partition atlease 4 gb of volume storage
1. `/dev/vdb1` 
2. `/dev/vdb2`

Make sure the device is seleted in the default varaible file and varaibles
other thing is to keep the default key is set in all the hsots in the inventory and try to ssh in all of your nodes

you need to define these 4 gorups of hosts in you inventory
1. `[admin]`
2. `[mons]`
3. `[osd1]`
4. `[osd2]`

#### Firstly clone the repo by thr following commnd

``` bash
git clone https://github.com/Vortexdude/ceph-storage

```
#### And go the ansible directory

``` bash
cd ansible/
```

and also need to define the logical volumes and other variable in [group_var/all](https://github.com/Vortexdude/ceph-storage/blob/master/ansible/group_vars/all.yml)

``` yml
logicalvolume1:
  external_device: /dev/vdb
  partition_index: 1
  lv_name: lv_ceph
  vg_name: vg_ceph
  partition_size: 20
  lvm_size: 10

logicalvolume2:
  external_device: /dev/vdb
  partition_index: 2
  lv_name: lv_ceph_40
  vg_name: vg_ceph_40
  partition_size: 50
  lvm_size: 40
```
In the above variable file define the storage size of patition and logical volme and group nanmes

#### Creating ceph-storage cluster run the ansible playbook make sure you install ansible in your host
``` bash
ansible-playbook main.yml
```



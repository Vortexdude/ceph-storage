# ceph-storage
### This ansible playbook is used for the setup the ceph-storage cluster
you need to define these 4 gorups of hosts in you inventory
1. [admin]
2. [mons]
3. [osd1]
4. [osd2]

#### firstly clone the repo by thr following commnd

``` bash
git clone https://github.com/Vortexdude/ceph-storage

```
#### and go the ansible directory

``` bash
cd ansible/
```

and also need to define the logical volumes and other variable in `groups variable`

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
in the above variable file define the storage size of patition and logical volme and group nanmes

#### Creating ceph-storage cluster run the ansible playbook make sure you install ansible in your host
``` bash
ansible-playbook main.yml
```


